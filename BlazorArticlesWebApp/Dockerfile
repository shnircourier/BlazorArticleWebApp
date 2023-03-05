FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["BlazorArticlesWebApp/BlazorArticlesWebApp.csproj", "BlazorArticlesWebApp/"]
RUN dotnet restore "BlazorArticlesWebApp/BlazorArticlesWebApp.csproj"
COPY . .
WORKDIR "/src/BlazorArticlesWebApp"
RUN dotnet build "BlazorArticlesWebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlazorArticlesWebApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlazorArticlesWebApp.dll"]
