# Examples and Templates

## Port contracts

```php
interface LoadOrderPort
{
    public function byId(OrderId $id): ?Order;
}

interface SaveOrderPort
{
    public function save(Order $order): void;
}
```

## Application use case

```php
final class ConfirmOrderUseCase
{
    public function __construct(
        private LoadOrderPort $loadOrder,
        private SaveOrderPort $saveOrder,
        private AppendOutboxMessagePort $appendOutbox,
        private TransactionRunnerPort $tx,
    ) {}

    public function handle(ConfirmOrderCommand $command): void
    {
        $this->tx->run(function () use ($command) {
            $order = $this->loadOrder->byId(new OrderId($command->orderId));
            $order->confirm();

            $this->saveOrder->save($order);
            $this->appendOutbox->append(new OrderConfirmedEvent($command->orderId));
        });
    }
}
```

## Infrastructure adapter sketch

```php
final class EloquentOrderRepository implements LoadOrderPort, SaveOrderPort
{
    public function byId(OrderId $id): ?Order
    {
        $record = OrderModel::query()->find($id->value());
        return $record ? OrderMapper::toDomain($record) : null;
    }

    public function save(Order $order): void
    {
        $record = OrderModel::query()->findOrNew($order->id()->value());
        OrderMapper::toRecord($order, $record);
        $record->save();
    }
}
```

## Decision checklist before coding

- Is domain free from infrastructure types?
- Are port contracts explicit and minimal?
- Can adapter be replaced without touching use case code?
