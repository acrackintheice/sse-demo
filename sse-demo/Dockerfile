FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["sse-demo/sse-demo.csproj", "sse-demo/"]
RUN dotnet restore "sse-demo/sse-demo.csproj"
COPY . .
WORKDIR "/src/sse-demo"
RUN dotnet build "sse-demo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "sse-demo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "sse-demo.dll"]
