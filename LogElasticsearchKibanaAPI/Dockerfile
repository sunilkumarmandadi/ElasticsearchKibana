#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["LogElasticsearchKibanaAPI/LogElasticsearchKibanaAPI.csproj", "LogElasticsearchKibanaAPI/"]
RUN dotnet restore "LogElasticsearchKibanaAPI/LogElasticsearchKibanaAPI.csproj"
COPY . .
WORKDIR "/src/LogElasticsearchKibanaAPI"
RUN dotnet build "LogElasticsearchKibanaAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LogElasticsearchKibanaAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LogElasticsearchKibanaAPI.dll"]