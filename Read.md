# UFSCzam

Sistema de identificação musical por fingerprinting de áudio.
Projeto final da disciplina de Sistemas Multimídia (CIT7596) — UFSC Araranguá, 2026.1.

## Problema

Identificar uma música a partir de um pequeno trecho de áudio captado pelo
ambiente, mesmo na presença de ruído, eco e compressão dos alto-falantes.
A comparação direta entre formas de onda é inviável; é necessário extrair
do sinal uma assinatura compacta e robusta.

## Solução

Implementação em Python do algoritmo de fingerprinting de áudio descrito por
Wang (2003) — o mesmo que fundamenta o serviço Shazam. O sistema cadastra
previamente um acervo de músicas, gera assinaturas digitais (hashes) baseadas
em picos espectrais e identifica trechos comparando-os contra esse banco.

## Tecnologias

- **Python 3.10+**
- **Librosa** — carregamento de áudio e STFT
- **NumPy** — manipulação de arrays
- **SciPy** — detecção de picos (filtro máximo 2D)
- **Sounddevice** — captura de áudio pelo microfone
- **Matplotlib** — visualização de espectrograma e constellation map

## Metodologia

1. **STFT** — áudio é convertido em espectrograma (tempo × frequência).
2. **Detecção de picos** — pontos de máxima energia local são identificados,
   formando o *constellation map*.
3. **Hashing combinatório** — cada pico é combinado com seus 15 vizinhos
   seguintes; cada par vira um hash `(freq1, freq2, delta_t)`.
4. **Busca por offset** — os hashes do trecho de consulta são comparados
   contra o banco; a música com mais hashes alinhados no mesmo offset
   temporal é a identificada.

## Estrutura prevista

```
echoprint/
├── musicas/                       # acervo de áudios
├── fingerprints.pkl               # banco gerado
├── fingerprint.py                 # motor (STFT, picos, hashes)
├── cadastrar.py                   # processa o acervo
├── identificar_arquivo.py         # identifica via arquivo
├── identificar_microfone.py       # identifica via microfone (demo)
├── visualizar.py                  # gera gráficos para o documento
├── requirements.txt
└── README.md
```

## Resultados esperados

- Taxa de acerto próxima de 100% em identificações a partir de arquivo (sem ruído).
- Taxa de acerto alta em gravações pelo microfone em ambiente moderadamente
  silencioso, com trechos a partir de ~10 segundos.
- Tempo de resposta inferior a 3 segundos para acervos de até 30 músicas.

## Cronograma

| Etapa | Prazo |
|---|---|
| Implementação do motor de fingerprinting | Semana 1 |
| Scripts de cadastro e identificação por arquivo | Semana 2 |
| Captura pelo microfone e testes | Semana 3 |
| Documento final, prints e ajustes | Semana 4 |
| **Entrega** | **17/06/2026** |

## Referências

- WANG, A. *An Industrial-Strength Audio Search Algorithm.* ISMIR, 2003.
- McFEE, B. et al. *librosa: Audio and Music Signal Analysis in Python.*
  Proceedings of the 14th Python in Science Conference, 2015.

---

**Autor:** [seu nome]
**Disciplina:** Sistemas Multimídia (CIT7596)
**Professora:** Marina Carradore Sérgio
