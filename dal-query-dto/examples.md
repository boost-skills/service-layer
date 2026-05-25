# Examples and Templates

## Repository contract (write side)

```php
interface OrderWriteRepository
{
    public function nextIdentity(): string;
    public function save(Order $order): void;
    public function getById(OrderId $id): ?Order;
}
```

## Query object (read side)

```php
final class SearchOrdersQuery
{
    public function __construct(
        public readonly ?int $customerId,
        public readonly ?string $status,
        public readonly int $limit = 50,
        public readonly int $offset = 0,
    ) {}
}
```

```php
interface SearchOrders
{
    /** @return list<OrderListItemData> */
    public function handle(SearchOrdersQuery $query): array;
}
```

## DTO output

```php
final class OrderListItemData
{
    public function __construct(
        public readonly int $id,
        public readonly string $number,
        public readonly string $status,
        public readonly string $total,
    ) {}
}
```

## Service orchestration

```php
final class ConfirmOrderService
{
    public function __construct(
        private OrderWriteRepository $orders,
        private OutboxWriter $outbox,
    ) {}

    public function handle(ConfirmOrderData $data): void
    {
        DB::transaction(function () use ($data) {
            $order = $this->orders->getById(new OrderId($data->orderId));
            $order->confirm();

            $this->orders->save($order);
            $this->outbox->append(new OrderConfirmedEvent($order->id()->value()));
        });
    }
}
```

## Decision checklist before coding

- Is this read concern better as a query object than repository method?
- Is output shape explicit and typed?
- Is transaction boundary visible at use-case level?
