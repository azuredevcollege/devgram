Wir wollen für den PoC CQRS Ansatz evaluieren, da damit Schreib- und Lesezugriffe unterschiedlich skalierbar wären. 

**Lastannahmen**
- Lesend: 1000 req/sek
- Schreibend: 100 req/sek

**API/Messages** 
- [POST]/API/Content/ -> CreateContentCommand { Content } -> CosmosDB (as EventStore) -> ContentCreated
- [PUT]/API/Content/ -> CreateContentCommand { Content } -> CosmosDB (as EventStore) -> ContentUpdated

- [GET]/API/Content/Query -> ContentQueryService (Materialized View, die ContentCreated,ContentUpdated,ContentDeleted subscribed und die DataView aufbaut)
  - GetById
  - GetByUserId
  - GetByLocation
  - GetByText
  - GetByTag...

**Collections**  
Die DomainOjects werden in CosmosDB Collections persistiert:
- ContentById (PartitionKey ContentId)
- ContentByUserId (PartitionKey UserId)
- ...

- API als AzureFunctions 
- .... @andreasmock bitte den Ablauf vervollständigen

// ToDO
@4iter4life klärt wegen der Subcsription mit MW TI
@codeunicorn bereinigt Readme
