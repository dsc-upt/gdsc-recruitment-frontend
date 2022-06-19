FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["GdscRecruitmentFrontend/GdscRecruitmentFrontend.csproj", "GdscRecruitmentFrontend/"]
RUN dotnet restore "GdscRecruitmentFrontend/GdscRecruitmentFrontend.csproj"
COPY . .
WORKDIR "/src/GdscRecruitmentFrontend"
RUN dotnet build "GdscRecruitmentFrontend.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "GdscRecruitmentFrontend.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "GdscRecruitmentFrontend.dll"]
