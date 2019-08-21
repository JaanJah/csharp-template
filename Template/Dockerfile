FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY TemplateConsole/*.csproj ./TemplateConsole/
WORKDIR /app/TemplateConsole
RUN dotnet restore


# Copy and publish app and libraries
WORKDIR /app/
COPY TemplateConsole/. ./TemplateConsole/
WORKDIR /app/TemplateConsole
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/runtime:2.2 AS runtime
WORKDIR /app
COPY --from=build /app/TemplateConsole/out ./
ENTRYPOINT ["dotnet", "TemplateConsole.dll"]
