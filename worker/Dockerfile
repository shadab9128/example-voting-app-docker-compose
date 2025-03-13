FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /code

# Copy the project file and restore dependencies
COPY Worker.csproj ./
RUN dotnet restore

# Copy the entire source code
COPY . ./

# Build and publish the application
RUN dotnet publish -c Release -o /code/out

# Use a lightweight runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
COPY --from=build /code/out .

# Set the entry point
CMD ["dotnet", "Worker.dll"]

