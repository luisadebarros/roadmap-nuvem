# 🌸 Roadmaps de Nuvem

Roadmap interativo dos meus estudos de nuvem, com três trilhas:

- **Microsoft Learn**: AZ-900 → .NET → dados → AI-200 → IA → DevOps
- **AWS**: Cloud Practitioner → IAM → serverless → containers → Developer Associate (DVA-C03) → IA → arquitetura
- **Docker & Kubernetes**: Docker → Dockerfile → Compose → segurança e CI → Kubernetes → Helm → CKAD → AKS/EKS/GKE → GitOps e observabilidade

Cada item leva direto para a página oficial de estudo. Marque o que já concluiu: o progresso fica salvo no navegador (localStorage), separado por trilha.

## Stack

HTML, CSS e JavaScript puros, num arquivo só e sem dependências nem build. Funciona em modo claro e escuro e se adapta ao celular.

## Rodar localmente

Abra o `index.html` no navegador.

## Personalizar

O conteúdo fica nos arrays `STOPS` e `TOOLS` de cada trilha (blocos `MS`, `AWS` e `K8S`), dentro do `<script>` de `index.html`. Cada item tem o formato:

```js
{ t: 'Título', k: 'trilha' | 'modulo' | 'docs' | 'video' | 'pratica', url: 'https://...', note: 'opcional' }
```

---

Feito por [Luísa de Barros Senra](https://github.com/luisadebarros)
