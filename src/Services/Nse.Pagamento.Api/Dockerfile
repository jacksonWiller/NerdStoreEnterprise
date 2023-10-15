#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["src/Services/Nse.Pagamento.Api/Nse.Pagamento.Api.csproj", "src/Services/Nse.Pagamento.Api/"]
RUN dotnet restore "src/Services/Nse.Pagamento.Api/Nse.Pagamento.Api.csproj"
COPY . .
WORKDIR "/src/src/Services/Nse.Pagamento.Api"
RUN dotnet build "Nse.Pagamento.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Nse.Pagamento.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Nse.Pagamento.Api.dll"]