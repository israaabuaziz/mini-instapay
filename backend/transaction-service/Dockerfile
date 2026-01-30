# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# Create and set working directory
WORKDIR /src

# Copy project file and restore dependencies
COPY transaction-service.csproj ./
RUN dotnet restore transaction-service.csproj --runtime linux-x64

# Copy everything else and build
COPY . .
RUN dotnet publish transaction-service.csproj -c Release -o /app/publish --runtime linux-x64 --self-contained false

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish ./
EXPOSE 5000
ENTRYPOINT ["dotnet", "transaction-service.dll"]
