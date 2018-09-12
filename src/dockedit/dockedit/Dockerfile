FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY dockedit/dockedit.csproj dockedit/
RUN dotnet restore dockedit/dockedit.csproj
COPY . .
WORKDIR /src/dockedit
RUN dotnet build dockedit.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish dockedit.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "dockedit.dll"]
