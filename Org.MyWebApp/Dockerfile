FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
# EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Org.MyWebApp.csproj", "."]
RUN dotnet restore "Org.MyWebApp.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "Org.MyWebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Org.MyWebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Org.MyWebApp.dll"]
