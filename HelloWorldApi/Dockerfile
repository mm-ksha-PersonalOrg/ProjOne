# Use the official .NET 8 SDK image for build
FROM mcr.microsoft.com/dotnet/sdk:8.0@sha256:874c4613d5ebf8b328ad920a90640c8dea9758bdbe61dc191dbcbed03721fc79 AS build
WORKDIR /src
COPY . .
RUN dotnet restore --locked-mode
RUN dotnet publish -c Release -o /app/publish --no-restore

# Use the official .NET 8 ASP.NET runtime image for runtime
FROM mcr.microsoft.com/dotnet/aspnet:9.0@sha256:925a86ec775fe737f1d65371ad7b2e01e81390c3c327ce3c06866a8ce8a4e1a2 AS final
WORKDIR /app
COPY --from=build /app/publish .
EXPOSE 8080
ENTRYPOINT ["dotnet", "HelloWorldApi.dll"]
