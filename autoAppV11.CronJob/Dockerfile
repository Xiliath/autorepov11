FROM mcr.microsoft.com/dotnet/runtime:8.0 AS base
WORKDIR /app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["autoAppV11.CronJob/autoAppV11.CronJob.csproj", "autoAppV11.CronJob/"]
RUN dotnet restore "autoAppV11.CronJob/autoAppV11.CronJob.csproj"
COPY . .
WORKDIR "/src/autoAppV11.CronJob"
RUN dotnet publish "autoAppV11.CronJob.csproj" -c Release -o /app/publish
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "autoAppV11.CronJob.dll"]