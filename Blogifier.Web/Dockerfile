FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 3000

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY Blogifier.sln ./
COPY Blogifier.Web/Blogifier.Web.csproj Blogifier.Web/
COPY Blogifier.Core/Blogifier.Core.csproj Blogifier.Core/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/Blogifier.Web
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENV ASPNETCORE_URLS http://*:3000
ENTRYPOINT ["dotnet", "Blogifier.Web.dll"]
