## 🧭 Project Conventions Guide

This guide outlines the core conventions used in our .NET project that follows Domain-Driven Design (DDD), Command Query Responsibility Segregation (CQRS), and clean architecture principles. All team members—especially newcomers—must follow these conventions to maintain code consistency, clarity, and quality.

---

### ✅ Endpoint Routing Convention

All API endpoint routes **must use kebab-case** (lowercase with hyphens) for consistency and readability.

#### ✅ Do:

```csharp
[Route("mass-upload-product-buying-price")]
```

#### ❌ Don't:

```csharp
[Route("MassUploadProductBuyingPrice")]
[Route("mass_upload_product_buying_price")]
[Route("massuploadproductbuyingprice")]
```

**Why:**
Kebab-case improves URL readability and is widely adopted in RESTful API design best practices.

---

### ✅ Use MediatR for Handling Requests

All request handling should go through **MediatR** by sending a command or query via the `Mediator` object. Avoid using service aggregators or custom orchestrators in controller actions.

#### ✅ Do:

```csharp
[HttpPut]
[Route("mass-upload-product-buying-price")]
public async Task<ActionResult> MassUploadProductBuyingPrice([FromForm] MassUploadProductBuyingPriceCommand command)
{
    await Mediator.Send(command);

    return Ok();
}
```

#### ❌ Don't:

```csharp
[HttpPost]
public async Task<ActionResult<Guid>> CreateStandard([FromForm] CreateProductVM request)
{
    var productId = await _aggregator.Create(request);

    return Ok(productId);
}
```

**Why:**
Using `Mediator.Send` enforces a consistent separation of concerns and aligns with CQRS principles. Avoiding aggregators ensures your controllers remain thin and orchestration logic stays in handlers.

---

### ✅ Use Descriptive and Unambiguous Names

Choose names that clearly describe the purpose and intent of the item (e.g., classes, methods, variables, commands). Avoid vague, abbreviated, or misleading names.

#### ✅ Do:

```csharp
public class MassUploadProductBuyingPriceCommand { }
public class GetCustomerInvoiceDetailsQuery { }
```

#### ❌ Don't:

```csharp
public class Command1 { }
public class GetData { }
public class CstmrQry { }
```

**Why:**
Clear and specific names improve code readability, make onboarding easier, and reduce the risk of misunderstandings or misuse.

---

### ✅ Replace Magic Numbers and Strings with Named Constants

Avoid using unexplained numeric or string literals ("magic numbers" or "magic strings") directly in your code. Instead, define and use **named constants** in a centralized static class for each logical area.

#### ✅ Do:

```csharp
namespace Talabeyah.Data.Common.Models
{
    public static class CustomerConstants
    {
        public const decimal MaxCustomerCompensation = 100;
        public const decimal MaxCustomerCashback = 100;
    }

    public static class SubRegions
    {
        public const string SubregionCreated = "events:subregion_created";
        public const string SubregionUpdated = "events:subregion_updated";
        public const string SubregionDeleted = "events:subregion_deleted";
    }
}
```

#### ❌ Don't:

```csharp
if (compensation > 100) { /* ... */ }
string topic = "events:subregion_created";
```

**Why:**
Named constants in a dedicated static class improve discoverability, enforce reusability, and make it easier to modify values in the future.

---

*More conventions will be added below as the project evolves.*
