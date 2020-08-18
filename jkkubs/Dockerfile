FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /jkkubs
COPY ["jkkubs/jkkubs.csproj", "jkkubs/"]

RUN dotnet restore "jkkubs/jkkubs.csproj"
COPY . .
WORKDIR "/src/jkkubs"
RUN dotnet build "jkkubs.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "jkkubs.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "jkkubs.dll"]