#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["abror_test.csproj", "abror_test/"]
RUN dotnet restore "abror_test/abror_test.csproj"
WORKDIR "/src/abror_test"
COPY . .
RUN dotnet build "abror_test.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "abror_test.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "abror_test.dll"]