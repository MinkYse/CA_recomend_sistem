FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER app
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["CA_recomend_sistem-api/CA_recomend_sistem-api.csproj", "CA_recomend_sistem-api/"]
RUN dotnet restore "./CA_recomend_sistem/CA_recomend_sistem.csproj"
COPY . .
WORKDIR "/src/CA_recomend_sistem"
RUN dotnet build "./CA_recomend_sistem-api.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./CA_recomend_sistem-api.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CA_recomend_sistem-api.dll"]
