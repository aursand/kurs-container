# Docker-container for "dummies" 

Så, du har laget en megakul app, men vil ikke bruke tusenvis av kroner, timer og tårer på å sette den opp på din lokale potetmasin i skapet på hybelen, samt at kompisne din, Roger, som du har slept deg med inn i en start-up hvor dere skal lage det neste Palworld-spillet, ikke har noe mer enn en chromebook fra 2015 å kjøre den eventuelle windows-appen dere skal lage. Da er docker løsningen for dere! I denne lille introen skal du få bygge din egen docker-container med noe kult inni, om du vil, for å så fyre den av opp mot skyen. 

## Så hva er Docker? 
Docker er en kontaineriserings-tjenste som gjør at man kan kjøre programmer og apper på dedikerte "servere" uavhengig av server-type, operativ-system eller annet trøbbel man måtte støte på hos sin lokale datamaskin. Dette gjør det også mulig å spare både plass, penger og svette, da man kan ha kjørende flere docker-tjenester samtidig lokalt, eller betale en slik og ingenting for å ha det kjørende i skyen. Mer info om selve Docker finner du på https://www.docker.com/ 

### Hva trenger du for å kjøre denne modulen? 
Det du trenger er:

1. en datamaskin med Visual Studio Code
2. Tilgang til et Azure-miljø
3. docker desktop (finnes her: https://www.docker.com/products/docker-desktop/)
4. Noe å bygge til en container

### Hallo, Docker! 
I denne modlulen har vi gitt en veldig enkel .NET app som gir en enkel teller eller ta ditt lokale prosjekt ut i en container! 

Det hele vil foregå i filen `Dockerfile` hvor man skal skrive en "oppskrift" som Docker skal kjøre etter. Den kan se slik ut:

```
FROM  mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
COPY bin/Debug/net7.0/DotNet.Docker.dll .
ENTRYPOINT [ "dotnet", "DotNet.Docker.dll" ]
```

Dette gir instruksjoner til Docker Engine om hvordan docker-filen skal oppføre seg. Denne filen skal hente ut ASPNET versjon 7.0 fra Microsoft sine nettsider via `FROM`-kommandoen, så sette `WORKDIR` til /app, altså hvor den skal starte appen fra. `COPY` kopierer en eller flere filer til `.` som vil se container-siden sin root-folder. 
`ENTRYPOINT` beskriver hvilken default-kommando docker-containeren skal starte med.

I dette tilfellet har vi et .NET prosjekt som må ha et SDK-image og en ASPNET runtime som er påkrevd for at containeren skal kjøre. 

Her kommer en stegvis visning i hvordan man kan få laget et image fra koden sin. 
1. Først må man publishe koden man allerede har for å generere binær-filer av koden. legg merke til at man får en `bin` og `obj` mappe i etterkant av `publish`.

```
dotnet publish -c Release  
```

2. nå kan man bygge docker-imaget med følgende kommando. Husk å bytte ut placeholder for et passende navn.

```
docker build -t <docker_image_navn> -f Dockerfile .
```

3. Etter det kan kan man nå lage en container med imaget i, følg med på docker desktop mens dette kjører for å se hva som dukker opp. 
```
docker create --name <docker_contianer_navn> <docker_image_navn>
```
4. Nå kan man starte containeren lokalt med `docker start`-kommandoen:
```
docker start <docker_contianer_navn>
```