FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY user-service.csproj ./
RUN dotnet restore user-service.csproj
COPY . ./
RUN dotnet publish user-service.csproj -c Release -o /app/publish
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/publish ./
EXPOSE 5000
ENTRYPOINT ["dotnet", "user-service.dll"]