FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY graphQLDotNetCore/graphQLDotNetCore.csproj graphQLDotNetCore/
RUN dotnet restore "graphQLDotNetCore/graphQLDotNetCore.csproj"
COPY . .
WORKDIR "/src/graphQLDotNetCore"
RUN dotnet build "graphQLDotNetCore.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "graphQLDotNetCore.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "graphQLDotNetCore.dll"]
