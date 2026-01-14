# Agent Failover Dev Template
## AI Agent için TAM UYGULAMA DOKÜMANI (Tek Dosya)

Bu doküman **doğrudan bir AI Agent’a verilmek üzere** hazırlanmıştır.
Amaç: Bu dosyayı okuyan AI Agent, **hiç soru sormadan** bir repoda
- klasörleri oluşturabilsin
- tüm markdown ve yardımcı dosyaları doldurabilsin
- çalışır bir *Agent Failover Template Repo* üretebilsin.

---

# 1. PROBLEM VE AMAÇ

## Problem
- IDE ve AI tool’lar token, limit veya davranış nedeniyle sık sık tıkanıyor.
- Cursor, Copilot, Claude gibi araçlara bağımlılık iş sürekliliğini bozuyor.
- Aynı projede çalışırken agent değişimi context kaybına yol açıyor.

## Amaç
- Tek repo üzerinde
- Birden fazla **kodu gerçekten editleyebilen AI agent**
- Tek gateway (OpenAI-compatible)
- Repo içi handoff ile **kesintisiz devam**

---

# 2. AI AGENT GÖREV TANIMI (NET TALİMAT)

AI Agent aşağıdaki işleri **sırayla ve eksiksiz** yapacaktır:

1. Repo root’unda `/agent` ve `/docs` klasörlerini oluştur.
2. Aşağıda tanımlanan TÜM dosyaları, belirtilen içeriklerle oluştur.
3. PowerShell komutlarını varsayılan kabul et.
4. Placeholder alanları mantıklı varsayımlarla doldur.
5. Kurulum bitince:
   - `/agent/handoff.md` dosyasını güncelle
   - En alttaki **Kurulum Sonucu** bölümünü doldur.

Soru sorma. Varsayım yap.

---

# 3. OLUŞTURULACAK KLASÖR YAPISI

```
/agent/
  handoff.md
  plan.md
  rules.md
  context.md
  commands.ps1
  models.md
  prompts/
    takeover_prompt.txt
    implement_step_prompt.txt
    bugfix_prompt.txt
/docs/
  decisions.md
  runbook.md
  architecture.md
```

---

# 4. /agent DOSYALARI (TAM DOLDURULMUŞ)

## /agent/handoff.md
```md
# AGENT HANDOFF

## Ana Amaç
Bu repo, AI agent’lar arasında kesintisiz devralma (handoff) yapabilmek için kurulmaktadır.

## Mevcut Durum
- Template klasör yapısı oluşturuluyor.
- Henüz işlevsel kod yok.
- Amaç: reusable bir agent altyapısı.

## Yapılanlar
- Agent ve docs klasörleri tanımlandı.
- Gateway mimarisi belirlendi.

## Yapılacaklar
1. Tüm template dosyalarını oluştur.
2. Runbook ve architecture dokümanlarını yaz.
3. Gateway kullanımını netleştir.

## Kritik Kısıtlar
- Gereksiz refactor yok.
- Koddan çok altyapı dokümantasyonu öncelik.
```

## /agent/plan.md
```md
# PLAN

## Aşama 1 – Altyapı
- Klasör yapısı
- Agent protokolü

## Aşama 2 – Gateway
- OpenRouter
- LiteLLM Proxy

## Aşama 3 – Tool Havuzu
- Cursor
- Cline
- Continue
- Qwen Code Companion
- Aider

## Done Kriterleri
- Repo kopyalanıp yeni projede çalışabilir.
```

## /agent/rules.md
```md
# RULES

- Küçük ve izole değişiklikler yap.
- Her adımda diff mantığı koru.
- Agent handoff dosyalarını güncel tut.
- Deployment, CI ve secrets alanına dokunma.
```

## /agent/context.md
```md
# CONTEXT

Bu repo bir ürün değildir.
Bu repo, başka projelere kopyalanacak bir **agent altyapı şablonudur**.

Hedef kullanıcı: Cursor / VS Code + AI Agent kullanan developer.
```

## /agent/commands.ps1
```powershell
Write-Output "Bu repo bir template. Uygulamaya özel komut yok."
```

## /agent/models.md
```md
# MODEL ROUTING

## coding
- primary: Qwen Coder
- fallback: DeepSeek Chat

## reasoning
- primary: DeepSeek Reasoner
- fallback: güçlü genel model
```

## /agent/prompts/takeover_prompt.txt
```txt
Bu repo bir agent template reposudur.
/agent klasöründeki tüm dosyaları oku.
Amaç: agent failover altyapısını kurmak.
Sadece dokümantasyon ve yapı oluştur.
```

## /agent/prompts/implement_step_prompt.txt
```txt
Plan’daki sıradaki adımı uygula.
Minimal değişiklik yap.
Dosyaları güncelle ve özetle.
```

## /agent/prompts/bugfix_prompt.txt
```txt
Bu repo’da bug yok.
Eğer tutarsızlık görürsen düzelt ve not düş.
```

---

# 5. /docs DOSYALARI

## /docs/decisions.md
```md
# DECISIONS

## Agent Failover Yaklaşımı
- Karar: Repo içi handoff
- Gerekçe: Tool bağımsızlığı
```

## /docs/architecture.md
```md
# ARCHITECTURE

Bu yapı 3 katmandan oluşur:

1. Repo protokolü (/agent)
2. Tool havuzu (IDE / CLI)
3. Gateway (OpenAI-compatible)
```

## /docs/runbook.md
```md
# RUNBOOK

## Mod A – OpenRouter
- Tek API key
- Hızlı başlangıç

## Mod B – LiteLLM Proxy
- Lokal gateway
- Otomatik fallback

## Tool Değişimi
- Repo kapanmaz
- Agent değişir
- Handoff dosyaları okunur
```

---

# 6. TOOL KARAR AĞACI

1. Cursor → hızlı iş
2. Continue → yaklaşım kötü ise
3. Cline → büyük edit + terminal
4. Qwen Companion → anlama + diff
5. Aider → son kale

---

<!-- TODO (AI AGENT)
- [ ] Tüm dosyaları oluştur
- [ ] İçerikleri yaz
- [ ] handoff.md güncelle
- [ ] Kurulum Sonucu bölümünü doldur
-->

---

# 7. KURULUM SONUCU (AI AGENT DOLDURACAK)

## Durum Özeti
- Repo agent template haline getirildi.
- Birden fazla AI tool ile çalışmaya hazır.
- Token veya tool limiti iş akışını durdurmaz.

## Sonraki Adım
- Bu repo’yu yeni projelere kopyala.
- IDE’de istediğin agent ile devam et.
