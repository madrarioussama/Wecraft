# Documentation API — OzoneExpress

## Ajouter Nouveau Colis

**Endpoint:**
```
POST https://api.ozonexpress.ma/customers/{YOUR_ID}/{YOUR_API_KEY}/add-parcel
```

---

## Paramètres (form-data)

| Paramètre | Requis | Description |
|---|---|---|
| `tracking-number` | Optionnel | Numéro de suivi personnalisé |
| `parcel-receiver` | **Requis** | Nom complet du destinataire |
| `parcel-phone` | **Requis** | Téléphone du destinataire |
| `parcel-city` | **Requis** | ID de la ville |
| `parcel-address` | **Requis** | Adresse complète |
| `parcel-note` | Optionnel | Instructions spéciales |
| `parcel-price` | **Requis** | Prix du colis en MAD |
| `parcel-declared-value` | Optionnel | Valeur déclarée en MAD (requis si prix vide, 0 ou > 5000 — min : 50) |
| `parcel-nature` | Optionnel | Description du contenu |
| `parcel-stock` | Optionnel | `1` = stock, `0` = ramassage |
| `parcel-open` | Optionnel | `1` = Ouvrir le colis, `2` = Ne pas ouvrir le colis (défaut : 1) |
| `parcel-fragile` | Optionnel | `1` = Oui, `0` = Non (défaut : 0) |
| `parcel-optional` | Optionnel | `1` = Oui, `0` = Non (défaut : 0) |
| `products` | Optionnel | JSON : `[{"ref": "PROD001", "qnty": 2}]` |

---

## Exemple cURL

```bash
curl -X POST "https://api.ozonexpress.ma/customers/12345/your-api-key/add-parcel" \
  -F "parcel-receiver=Mohammed Alami" \
  -F "parcel-phone=0612345678" \
  -F "parcel-city=1" \
  -F "parcel-address=123 Rue Hassan II" \
  -F "parcel-price=250" \
  -F "parcel-stock=1"
```

---

## Exemple PHP

```php
$curl = curl_init();
curl_setopt_array($curl, [
  CURLOPT_URL => "https://api.ozonexpress.ma/customers/12345/your-api-key/add-parcel",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_POST => true,
  CURLOPT_POSTFIELDS => [
    "parcel-receiver" => "Mohammed Alami",
    "parcel-phone"    => "0612345678",
    "parcel-city"     => "1",
    "parcel-address"  => "123 Rue Hassan II",
    "parcel-price"    => "250",
    "parcel-stock"    => "1"
  ]
]);
$response = curl_exec($curl);
curl_close($curl);
echo $response;
```

---

## Réponse JSON

```json
{
  "TRACKING-NUMBER": "OZE123456789",
  "RECEIVER": "Mohammed Alami",
  "PHONE": "0612345678",
  "CITY_ID": "1",
  "CITY_NAME": "Casablanca",
  "ADDRESS": "123 Rue Hassan II",
  "PRICE": "250",
  "DELIVERED-PRICE": "25",
  "RETURNED-PRICE": "15",
  "REFUSED-PRICE": "15"
}
```

---

## Ressources

- **Liste des villes :** https://api.ozonexpress.ma/cities

> **NOTE :** Trouvez votre clé API dans la section **Compte → Generate your API key**

---

## Zone de Test — Ajouter un Colis

| Champ | Valeur exemple |
|---|---|
| Votre ID Client | `12345` |
| Clé API | `votre-cle-api-ici` |
| Nom du destinataire | `Mohammed Alami` |
| Téléphone | `0612345678` |
| ID Ville | *(sélectionner depuis la liste)* |
| Adresse | `123 Rue Hassan II, Quartier Maarif` |
| Prix (MAD) | `250` |
| Valeur déclarée (MAD) | Min 50 — requis si prix vide ou > 5000 MAD |
| Type de colis | *(sélectionner)* |
| Ouverture de colis | *(optionnel)* |
| Fragile | *(optionnel)* |
| Échange | *(optionnel)* |
| Note | `Appeler avant livraison` |
