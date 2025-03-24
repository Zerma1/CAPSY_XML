## Cours sur XML (Extensible Markup Language)

### Introduction à XML
XML (Extensible Markup Language) est un langage de balisage utilisé pour structurer, stocker et transporter des données de manière lisible par les humains et les machines. Il est largement utilisé pour l’échange de données entre systèmes informatiques.

---

## 1. Structure de base d’un document XML
Un document XML est composé d’éléments qui forment une structure arborescente. Voici un exemple simple d’un fichier XML :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<livres>
	<livre>
		<titre>Les Misérables</titre>
		<auteur>Victor Hugo</auteur>
		<annee>1862</annee>
	</livre>
	<livre>
		<titre>1984</titre>
		<auteur>George Orwell</auteur>
		<annee>1949</annee>
	</livre>
</livres>
```

### Explication de la structure :
- `<?xml version="1.0" encoding="UTF-8"?>` → Déclaration XML.
- `<livres>` → Élément racine.
- `<livre>` → Élément parent contenant des sous-éléments (`<titre>`, `<auteur>`, `<annee>`).
- Chaque élément XML est délimité par une balise ouvrante (`<...>`) et une balise fermante (`</...>`).

---

## 2. Règles et syntaxe de XML
XML suit des règles strictes :
1. **Un élément doit être correctement fermé** :
   ```xml
   <nom>Jean Dupont</nom>  <!-- Correct -->
   <nom>Jean Dupont  <!-- Incorrect -->
   ```
2. **Les balises sont sensibles à la casse** :
   ```xml
   <Nom>Jean</Nom>  <!-- Différent de <nom>Jean</nom> -->
   ```
3. **Un seul élément racine** :
   ```xml
   <personnes>
	   <personne>Jean</personne>
	   <personne>Marie</personne>
   </personnes>
   ```
4. **Les attributs doivent être entre guillemets** :
   ```xml
   <livre titre="1984" auteur="George Orwell"/>
   ```

---

## 3. Utilisation des attributs et des éléments
Deux façons de stocker des informations :

- **Avec des éléments** :
  ```xml
  <livre>
	  <titre>1984</titre>
	  <auteur>George Orwell</auteur>
  </livre>
  ```
- **Avec des attributs** :
  ```xml
  <livre titre="1984" auteur="George Orwell"/>
  ```

💡 **Bonne pratique** : Utiliser les attributs pour les métadonnées et les éléments pour les données principales.

---

## 4. Validation d’un fichier XML
### 4.1. DTD (Document Type Definition)
Exemple d’une DTD :
```dtd
<!DOCTYPE livres [
	<!ELEMENT livres (livre+)>
	<!ELEMENT livre (titre, auteur, annee)>
	<!ELEMENT titre (#PCDATA)>
	<!ELEMENT auteur (#PCDATA)>
	<!ELEMENT annee (#PCDATA)>
]>
```

### 4.2. XSD (XML Schema Definition)
Exemple de schéma XSD :
```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
	<xs:element name="livres">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="livre" maxOccurs="unbounded">
					<xs:complexType>
						<xs:sequence>
							<xs:element name="titre" type="xs:string"/>
							<xs:element name="auteur" type="xs:string"/>
							<xs:element name="annee" type="xs:integer"/>
						</xs:sequence>
					</xs:complexType>
				</xs:element>
			</xs:sequence>
		</xs:complexType>
	</xs:element>
</xs:schema>
```

---

## 5. Manipulation XML en programmation
### 5.1. En Python avec `xml.etree.ElementTree`
```python
import xml.etree.ElementTree as ET

tree = ET.parse('livres.xml')
root = tree.getroot()

for livre in root.findall('livre'):
	titre = livre.find('titre').text
	auteur = livre.find('auteur').text
	print(f"Titre : {titre}, Auteur : {auteur}")
```

### 5.2. En Java avec DOM Parser
```java
import javax.xml.parsers.*;
import org.w3c.dom.*;

public class XMLReader {
	public static void main(String[] args) throws Exception {
		DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
		DocumentBuilder builder = factory.newDocumentBuilder();
		Document doc = builder.parse("livres.xml");

		NodeList livres = doc.getElementsByTagName("livre");
		for (int i = 0; i < livres.getLength(); i++) {
			Element livre = (Element) livres.item(i);
			String titre = livre.getElementsByTagName("titre").item(0).getTextContent();
			System.out.println("Titre : " + titre);
		}
	}
}
```

---

## 6. XML vs JSON
| **Caractéristique** | **XML** | **JSON** |
|---------------------|---------|----------|
| Lisibilité humaine  | Moyenne | Excellente |
| Poids des données   | Plus lourd | Plus léger |
| Validation		 | DTD/XSD | Aucun schéma imposé |
| Compatibilité	 | Standard ancien | Préféré pour le web |

---

## Conclusion
XML est un langage puissant pour structurer et échanger des données. Il est utilisé dans de nombreux domaines comme les bases de données, les services web (SOAP), et les fichiers de configuration. Cependant, JSON est souvent privilégié pour les applications modernes en raison de sa simplicité.

Tu veux approfondir un point en particulier ? 😊

