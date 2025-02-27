FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["autoAppV11.WebApi/autoAppV11.WebApi.csproj", "autoAppV11.WebApi/"]
RUN dotnet restore "autoAppV11.WebApi/autoAppV11.WebApi.csproj"
COPY . .
WORKDIR "/src/autoAppV11.WebApi"
RUN dotnet build "autoAppV11.WebApi.csproj" -c Release -o /app/build
FROM build AS publish
RUN dotnet publish "autoAppV11.WebApi.csproj" -c Release -o /app/publish
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "autoAppV11.WebApi.dll"]