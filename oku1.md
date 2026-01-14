# AI Agent Failover Dev Template – Tek Dosya Dokümantasyon

Bu doküman, aynı local repo üzerinde çalışırken **token/limit/providera takılmadan**, farklı **kodu gerçekten editleyebilen AI agent ve tool’lar** arasında hızlıca geçiş yapabilmek için hazırlanmış **tek dosyalık ana rehberdir**.

Amaç:  
**Tek repo + çok tool + tek gateway + standart handoff**

---

## 1) Problem Tanımı

- Cursor Plus var ama bazen token bitiyor veya yaklaşımı beğenilmiyor  
- Copilot limitleri dolu  
- Claude iptal edildi (token maliyeti)  
- Qwen çok iyi anlıyor ama tek başına edit yapamıyor  
- İş yarıda kalmasın, aynı projede başka agent hemen devralsın isteniyor  

---

## 2) Nihai Hedef

Kurulum bittiğinde:

- Aynı repo içinde **5–6 farklı edit-capable AI tool** kullanılabilir olacak  
- Bir tool/providera takılınca **başka tool ile devam edilebilecek**  
- Handoff sohbetten değil **repo içi dosyalardan** yapılacak  
- Tüm tool’lar **tek gateway** (OpenAI-compatible) üzerinden beslenecek  

---

## 3) Tool Havuzu (Edit Yapabilenler)

Bu yapı aşağıdaki araçları kapsar:

- Cursor Agent  
- VS Code: Cline  
- VS Code: Continue  
- VS Code: Roo Code (opsiyonel)  
- VS Code: Qwen Code Companion  
- Terminal: Aider  

Hepsi:
- Aynı repo üzerinde çalışır  
- Dosya oluşturabilir / değiştirebilir  
- Handoff dosyalarını okuyarak devralabilir  

---

## 4) Repo Template Yapısı

Aşağıdaki yapı her projeye eklenecek:

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
/docs/
  decisions.md
  runbook.md
  architecture.md
```

---

## 5) /agent Dosyaları

### /agent/handoff.md
```md
# AGENT HANDOFF

## Amaç
- ...

## Durum
- Yapılanlar:
- Yapılmayanlar:
- Blokajlar:

## Sıradaki Aksiyonlar
1) ...
2) ...

## Kritik Dosyalar
- ...

## Notlar
- Minimal değişiklik yap
- Unrelated refactor yok
```

### /agent/plan.md
```md
# PLAN

## Adımlar
1) ...
2) ...

## Done Kriterleri
- [ ] ...
```

### /agent/rules.md
```md
# RULES
- Küçük ve test edilebilir değişiklikler
- Diff özeti zorunlu
- Destructive komut yok
```

### /agent/context.md
```md
# CONTEXT
- Repo amacı
- Tech stack
- Önemli klasörler
```

### /agent/commands.ps1
```powershell
npm ci
npm run dev
npm run build
npm test
npm run lint
```

### /agent/models.md
```md
# MODEL ROUTING

Coding:
- Qwen Coder
- DeepSeek Chat (fallback)

Reasoning:
- DeepSeek Reasoner
```

### /agent/prompts/takeover_prompt.txt
```txt
Bu repo taskını devral.
/agent içindeki tüm md dosyalarını oku.
Sadece sıradaki aksiyonu uygula.
Minimal değişiklik yap ve diff sun.
```

---

## 6) /docs Dosyaları

### /docs/decisions.md
```md
# DECISIONS
- Karar / Gerekçe / Alternatif
```

### /docs/architecture.md
```md
# ARCHITECTURE
- Tek repo
- Çok tool
- Tek gateway
```

### /docs/runbook.md
```md
# RUNBOOK

## Mod A – OpenRouter
- Tek API key
- Tüm tool’lar aynı endpoint

## Mod B – LiteLLM Proxy
- Lokal OpenAI-compatible gateway
- Otomatik fallback
```

---

## 7) Gateway Mimarisi

### Mod A – OpenRouter
- En hızlı başlangıç
- Manuel model değişimi

### Mod B – LiteLLM Proxy
- Tüm tool’lar tek endpoint’e bağlanır
- coding → Qwen → DeepSeek fallback
- reasoning → DeepSeek → güçlü model fallback

---

## 8) Karar Ağacı (Hangi Tool Ne Zaman)

1) Cursor Agent – hızlı iterasyon  
2) Continue – sakin akış, model değişimi  
3) Cline – multi-file + terminal  
4) Qwen Code Companion – anlama güçlü, diff ile edit  
5) Roo Code – Cline alternatifi  
6) Aider – son kale, git/diff odaklı  

---

## 9) AI Agent Görev Listesi

<!-- TODO
- [ ] /agent ve /docs klasörlerini oluştur
- [ ] Tüm md dosyalarını ekle
- [ ] Runbook’a OpenRouter ve LiteLLM notlarını yaz
- [ ] Karar ağacını ekle
- [ ] Kurulum özetini doldur
-->

---

## 10) Kurulum Sonrası Basit Özet (AI Agent Dolduracak)

- Repo agent template ile hazırlandı.
- Birden fazla AI tool aynı repo’da kullanılabilir.
- Token veya tool limiti işleri durdurmaz.
- Bundan sonra agent değişse bile iş devam eder.
