# Étape 1 : Utiliser une image de base contenant .NET
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

# Étape 2 : Utiliser l'image SDK .NET pour la compilation
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Portfolio/Portfolio.csproj", "Portfolio/"]
RUN dotnet restore "Portfolio/Portfolio.csproj"
COPY . .
WORKDIR "/src/Portfolio"
RUN dotnet build "Portfolio.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Portfolio.csproj" -c Release -o /app/publish

# Étape 3 : Créer l'image finale
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Portfolio.dll"]
