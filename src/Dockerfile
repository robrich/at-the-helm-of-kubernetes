# build server
FROM mcr.microsoft.com/dotnet/sdk:8.0-alpine as build

WORKDIR /src

COPY AtTheHelm.csproj .
RUN dotnet restore

COPY . .
RUN dotnet build -c Release AtTheHelm.csproj
RUN dotnet test -c Release AtTheHelm.csproj
RUN dotnet publish -c Release -o /dist AtTheHelm.csproj


# production runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0-alpine

ENV ASPNETCORE_ENVIRONMENT Production
ENV ASPNETCORE_URLS http://+:80
EXPOSE 80

WORKDIR /app
COPY --from=build /dist .

CMD ["dotnet", "AtTheHelm.dll"]
