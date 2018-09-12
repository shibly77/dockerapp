FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY dockcity/dockcity.csproj dockcity/
RUN dotnet restore dockcity/dockcity.csproj
COPY . .
WORKDIR /src/dockcity
RUN dotnet build dockcity.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish dockcity.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "dockcity.dll"]
