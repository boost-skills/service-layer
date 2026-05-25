# Service Templates and Examples

## Service Class Template

```php
<?php

declare(strict_types=1);

namespace App\Services\Orders;

use App\Contracts\Payments\PaymentGateway;
use App\DataTransferObjects\Orders\CreateOrderData;
use App\Models\Order;
use Illuminate\Support\Facades\DB;

final class CreateOrderService
{
    public function __construct(
        private PaymentGateway $paymentGateway,
    ) {}

    public function handle(CreateOrderData $data): Order
    {
        return DB::transaction(function () use ($data): Order {
            $order = Order::query()->create([
                'user_id' => $data->userId,
                'status' => 'pending',
                'total' => $data->total,
            ]);

            $paymentId = $this->paymentGateway->authorize($order, $data->paymentToken);

            $order->forceFill(['payment_id' => $paymentId])->save();

            return $order->fresh();
        });
    }
}
```

## DTO Template

```php
<?php

declare(strict_types=1);

namespace App\DataTransferObjects\Orders;

final readonly class CreateOrderData
{
    public function __construct(
        public int $userId,
        public string $paymentToken,
        public int $total,
    ) {}
}
```

## Contract Template

```php
<?php

declare(strict_types=1);

namespace App\Contracts\Payments;

use App\Models\Order;

interface PaymentGateway
{
    public function authorize(Order $order, string $paymentToken): string;
}
```

## Controller Usage Template

```php
<?php

declare(strict_types=1);

namespace App\Http\Controllers;

use App\DataTransferObjects\Orders\CreateOrderData;
use App\Http\Requests\Orders\StoreOrderRequest;
use App\Services\Orders\CreateOrderService;
use Illuminate\Http\JsonResponse;

final class StoreOrderController
{
    public function __invoke(
        StoreOrderRequest $request,
        CreateOrderService $service,
    ): JsonResponse {
        $data = new CreateOrderData(
            userId: (int) $request->user()->id,
            paymentToken: (string) $request->validated('payment_token'),
            total: (int) $request->validated('total'),
        );

        $order = $service->handle($data);

        return response()->json([
            'id' => $order->id,
            'status' => $order->status,
        ]);
    }
}
```

## Provider Binding Template

```php
<?php

declare(strict_types=1);

namespace App\Providers;

use App\Contracts\Payments\PaymentGateway;
use App\Infrastructure\Payments\StripePaymentGateway;
use Illuminate\Support\ServiceProvider;

final class PaymentServiceProvider extends ServiceProvider
{
    public function register(): void
    {
        $this->app->bind(PaymentGateway::class, StripePaymentGateway::class);
    }
}
```
