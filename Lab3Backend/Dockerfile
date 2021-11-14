#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Lab3Backend/Lab3Backend.csproj", "Lab3Backend/"]
RUN dotnet restore "Lab3Backend/Lab3Backend.csproj"
COPY . .
WORKDIR "/src/Lab3Backend"
RUN dotnet build "Lab3Backend.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Lab3Backend.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Lab3Backend.dll"]