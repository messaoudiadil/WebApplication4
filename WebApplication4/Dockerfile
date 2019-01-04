FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 8080

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY *.csproj ./
RUN dotnet restore "WebApplication4.csproj"
COPY . ./
#WORKDIR /src/WebApplication4  "WebApplication4.csproj"
RUN dotnet build  -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebApplication4.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication4.dll"]