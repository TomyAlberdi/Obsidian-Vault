Created: 2024-09-17 16:57
## Family Tree:
1. Computer
2. [[Programming Theory]]
-- -
We will now look at how to structure our projects following **Domain-Driven Design (DDD)**. This approach helps us structure and model Software based on the domain it belongs to, where each folder (or folder structure) has its specific purpose.
## Principles
- Place the organization's **business models** and **rules** at the core of the application.
- Base a complex domain on a **software model**.
- Promote better collaboration between **domain experts** and **developers**, with the goal of creating software with clear objectives.
## Structure
- **`/cmd`**: This folder contains the entry points of the main application. Each entry point will be a package inside the `cmd` folder and will have its own Go file: `main.go`, along with the necessary code (configurations, environments, dependency injection, etc.). It’s important to note that the packages inside `cmd` must correspond to the name of the entry points, i.e., the names of the respective application binaries.
- **`/internal`**: This package contains the private library code that is used within your service. It is specific to the service's functionality and is not shared with other services.
- **`/pkg`**: This folder contains code that can be consumed by other services. This may include API clients or useful functions for other services.