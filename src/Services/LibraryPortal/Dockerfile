#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/Services/LibraryPortal/LibraryPortal.csproj", "src/Services/LibraryPortal/"]
RUN dotnet restore "src/Services/LibraryPortal/LibraryPortal.csproj"
COPY . .
WORKDIR "/src/src/Services/LibraryPortal"
RUN dotnet build "LibraryPortal.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LibraryPortal.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LibraryPortal.dll"]
