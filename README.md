```plantuml
@startuml
class SV{
  #id: int
  #name: string
  #age : int
  
  +SV(id,name,int)
  
}
class SVIT{
  -sad: float
  -se: float
  
  +DTB(): float
}

SV <|-- SVIT




@enduml
