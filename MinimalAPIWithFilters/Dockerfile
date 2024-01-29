FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["MinimalAPIWithFilters/MinimalAPIWithFilters.csproj", "MinimalAPIWithFilters/"]
RUN dotnet restore "MinimalAPIWithFilters/MinimalAPIWithFilters.csproj"
COPY . .
WORKDIR "/src/MinimalAPIWithFilters"
RUN dotnet build "MinimalAPIWithFilters.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MinimalAPIWithFilters.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MinimalAPIWithFilters.dll"]
