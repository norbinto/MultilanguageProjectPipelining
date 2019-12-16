FROM posannorbert/usqc:1.0-alpine3.10 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM posannorbert/usqcsdk:1.0-alpine3.10 AS build
WORKDIR /src
COPY ["MultilanguageProjectPipelining.Web/MultilanguageProjectPipelining.Web.csproj", "MultilanguageProjectPipelining.Web/"]
RUN dotnet restore "MultilanguageProjectPipelining.Web/MultilanguageProjectPipelining.Web.csproj"
COPY . .
WORKDIR "/src/MultilanguageProjectPipelining.Web"
RUN dotnet build "MultilanguageProjectPipelining.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MultilanguageProjectPipelining.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MultilanguageProjectPipelining.Web.dll"]