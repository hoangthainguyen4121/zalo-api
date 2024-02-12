#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Zalo.Tet.Api/Zalo.Tet.Api.csproj", "Zalo.Tet.Api/"]
RUN dotnet restore "Zalo.Tet.Api/Zalo.Tet.Api.csproj"
COPY . .
WORKDIR "/src/Zalo.Tet.Api"
RUN dotnet build "Zalo.Tet.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Zalo.Tet.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Zalo.Tet.Api.dll"]