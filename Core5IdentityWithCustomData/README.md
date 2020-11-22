# Project

This is demo project to show how to add custom data in .net core 5. There is no different with .Net core 3.1. I will do more testing to add custom role etc to check all identity framework features.

## Steps

* Add custom data

```cs
public class AppUser : IdentityUser
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

* Add DB Context

```cs
public class AppIdentityDbContext : IdentityDbContext<AppUser>
{
    public AppIdentityDbContext(DbContextOptions<AppIdentityDbContext> options) : base(options) { }
}
```

* Update connection string

```json
"ConnectionStrings": {
    "DefaultConnection": "Server=(localhost);Database=yourdatabase;Trusted_Connection=True;MultipleActiveResultSets=true"
  }
```

* Update Startup.cs

```cs
services.AddDbContext<AppIdentityDbContext>(options =>
    options.UseSqlServer(
        Configuration.GetConnectionString("DefaultConnection")));

services.AddIdentity<AppUser, IdentityRole>().AddEntityFrameworkStores<AppIdentityDbContext>().AddDefaultTokenProviders();

```

* Update database

```powershell
update-database
```
