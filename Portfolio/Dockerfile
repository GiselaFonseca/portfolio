# Utilise l'image officielle de .NET comme image de base
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

# Utilise l'image SDK de .NET pour la phase de build
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Portfolio/Portfolio.csproj", "Portfolio/"]
RUN dotnet restore "Portfolio/Portfolio.csproj"
COPY . .
WORKDIR "/src/Portfolio"
RUN dotnet build "Portfolio.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Portfolio.csproj" -c Release -o /app/publish

# Exécute l'application
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Portfolio.dll"]
