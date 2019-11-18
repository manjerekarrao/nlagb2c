FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["nlagb2c/nlagb2c.csproj", "nlagb2c/"]
RUN dotnet restore "nlagb2c/nlagb2c.csproj"
COPY . .
WORKDIR "/src/nlagb2c"
RUN dotnet build "nlagb2c.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "nlagb2c.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "nlagb2c.dll"]