FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

COPY report.csproj ./
RUN dotnet restore report.csproj

COPY . ./ 

RUN dotnet publish report.csproj -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

COPY --from=build /app/publish ./

EXPOSE 5000
ENTRYPOINT ["dotnet", "report.dll"]