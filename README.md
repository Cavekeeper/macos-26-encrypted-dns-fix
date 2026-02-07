# macOS 26.2 Encrypted-DNS Fix (dnsforge.de & andere)

Dieses Repository enthält einen Workaround für die Installation von DNS-over-HTTPS (DoH) und DNS-over-TLS (DoT) Profilen unter **macOS 26.2 (Tahoe)**.

## Das Problem
In macOS 26.2 schlägt die Installation herkömmlicher `.mobileconfig`-Profile oft fehl. Das System meldet, dass der "VPN-Dienst" nicht erstellt werden konnte, obwohl es sich um ein reines DNS-Profil handelt.

## Der Fix
Das Profil muss explizit den Geltungsbereich `System` deklarieren. 

### Anleitung
1. Lade die Datei `dnsforge-fix.mobileconfig` aus diesem Repo herunter.
2. Öffne die **Systemeinstellungen** > **Datenschutz & Sicherheit** > **Profile**.
3. Klicke auf das `+` Symbol und wähle die Datei aus.
4. Falls gefragt wird: Bestätige die Installation für "Alle Benutzer" (System-Ebene).

## Manuelle Anpassung für andere Dienste
Falls du einen anderen Anbieter (z.B. Quad9 oder AdGuard) nutzt, öffne deine `.mobileconfig` in einem Texteditor und füge direkt unter dem ersten `<dict>`-Tag folgendes ein:

```xml
<key>PayloadScope</key>
<string>System</string>
```
### Zusammenfassung der Änderungen
* **PayloadScope**: Muss auf `System` gesetzt sein.
* **Admin-Rechte**: Da es nun ein System-Profil ist, wird bei der Installation zwingend das Admin-Passwort oder Touch ID verlangt.
* **Vermeidung von VPN-Konflikten**: Durch diesen Hack erkennt macOS, dass es sich um eine Netzwerkkonfiguration auf Systemebene handelt und nicht um einen fehlerhaften User-VPN-Tunnel.
