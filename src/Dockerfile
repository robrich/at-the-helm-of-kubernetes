# build server
FROM mcr.microsoft.com/dotnet/sdk:6.0-alpine as build

WORKDIR /src

COPY AtTheHelm.csproj .
RUN dotnet restore

COPY . .
RUN dotnet build -c Release
RUN dotnet test -c Release
RUN dotnet publish -c Release -o /dist


# production runtime
FROM mcr.microsoft.com/dotnet/aspnet:6.0-alpine

ENV ASPNETCORE_ENVIRONMENT Production
ENV ASPNETCORE_URLS http://+:80
EXPOSE 80

WORKDIR /app
COPY --from=build /dist .

CMD ["dotnet", "AtTheHelm.dll"]
