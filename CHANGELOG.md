# Changelog

Tutte le modifiche rilevanti a questo modulo sono documentate in questo file.

Il formato è basato su [Keep a Changelog](https://keepachangelog.com/it/1.1.0/)
e questo progetto aderisce al [Semantic Versioning](https://semver.org/lang/it/).

## [1.0.0] - 2026-11-02

### Added
- Invio del **numero di tracking** al cliente su **WhatsApp** tramite l'API template di **Infobip**: un messaggio per ogni
  nuovo tracking di spedizione, con numero d'ordine, corriere e codice di tracking.
- Cron ogni 15 minuti (massimo 200 messaggi per esecuzione). **Spento di default**.
- Configurazione per store view in *Negozi → Configurazione → Threecommerce Plugins → WhatsApp Infobip*: URL API,
  API Key (cifrata), mittente, nome e lingua del template, prefisso internazionale predefinito, data di partenza, log di debug.
- Numero di telefono dell'indirizzo di spedizione portato in formato internazionale (spazi, `+`, `00` e zero iniziale gestiti).
- Esito tracciato in `sales_shipment_track.whatsapp_send`: vuoto = da inviare, `1` = inviato, `2` = scartato
  (numero non valido o messaggio rifiutato). Gli errori temporanei (rete, 5xx, 429) e di credenziali (401/403) vengono ritentati.
- *Invia tracking creati dal* è impostata alla data di installazione: i tracking precedenti non vengono mai inviati.

### Changed (rispetto al modulo interno `Gp_WhatsappInfobip`)
- Il pacchetto diventa `threecommerce/m2-whatsapp-infobip` e la configurazione passa dalla sezione `infobip/general/*`
  a `threecommerce_infobip/general/*`. Il campo `num_tel` si chiama ora `sender` e `lang` si chiama `language`.
- I segnaposto del template sono posizionali: `{{1}}` ordine, `{{2}}` corriere, `{{3}}` tracking.
