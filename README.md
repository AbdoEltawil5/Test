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

*More conventions will be added below as the project evolves.*
