FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["CoreTest/CoreTest.csproj", "CoreTest/"]
RUN dotnet restore "CoreTest/CoreTest.csproj"
COPY . .
WORKDIR "/src/CoreTest"
RUN dotnet build "CoreTest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CoreTest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CoreTest.dll"]