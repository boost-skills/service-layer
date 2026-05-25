# Examples and Templates

## Service with explicit transaction

```php
final class ApproveInvoiceService
{
    public function handle(ApproveInvoiceData $data): void
    {
        DB::transaction(function () use ($data) {
            $invoice = Invoice::query()
                ->whereKey($data->invoiceId)
                ->lockForUpdate()
                ->firstOrFail();

            $invoice->approve($data->approvedBy);
            $invoice->save();
        });
    }
}
```

## Reusable scope

```php
class Invoice extends Model
{
    public function scopeForDashboard(Builder $query): Builder
    {
        return $query->with(['customer:id,name'])
            ->select(['id', 'number', 'customer_id', 'status', 'total']);
    }
}
```

## Query service for complex read model

```php
final class InvoiceReportQuery
{
    /** @return list<InvoiceReportRowData> */
    public function handle(InvoiceReportFilter $filter): array
    {
        return Invoice::query()
            ->when($filter->from, fn ($q) => $q->whereDate('issued_at', '>=', $filter->from))
            ->when($filter->to, fn ($q) => $q->whereDate('issued_at', '<=', $filter->to))
            ->orderByDesc('issued_at')
            ->limit($filter->limit)
            ->get()
            ->map(fn (Invoice $invoice) => new InvoiceReportRowData(
                id: $invoice->id,
                number: $invoice->number,
                status: $invoice->status,
                total: (string) $invoice->total,
            ))
            ->all();
    }
}
```

## Decision checklist before coding

- Is Eloquent enough for this use case today?
- Is there a clear loading strategy for relations?
- Do we need transaction + after-commit side effects?
