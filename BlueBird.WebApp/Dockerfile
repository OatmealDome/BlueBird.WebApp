FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["BlueBird.WebApp/BlueBird.WebApp.csproj", "BlueBird.WebApp/"]
RUN dotnet restore "BlueBird.WebApp/BlueBird.WebApp.csproj"
COPY . .
WORKDIR "/src/BlueBird.WebApp"
RUN dotnet build "BlueBird.WebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlueBird.WebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlueBird.WebApp.dll"]
