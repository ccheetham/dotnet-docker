---
actions:
  to: Dockerfile
---
FROM mcr.microsoft.com/dotnet/aspnet:{{dotNetVersion}} AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:{{dotNetVersion}} AS build
WORKDIR /src
COPY ["{{artifactId}}.csproj", "."]
RUN dotnet restore "{{artifactId}}.csproj"
COPY . .
RUN dotnet build "{{artifactId}}.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "{{artifactId}}.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "{{artifactId}}.dll"]
