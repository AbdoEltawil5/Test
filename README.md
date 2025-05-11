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

*More conventions will be added below as the project evolves.*
