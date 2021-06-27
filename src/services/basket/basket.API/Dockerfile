#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["services/basket/basket.API/basket.API.csproj", "services/basket/basket.API/"]
RUN dotnet restore "services/basket/basket.API/basket.API.csproj"
COPY . .
WORKDIR "/src/services/basket/basket.API"
RUN dotnet build "basket.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "basket.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "basket.API.dll"]
