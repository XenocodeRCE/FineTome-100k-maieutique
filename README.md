# 🧘 FineTome-100k-maieutique
Une version custom de [https://huggingface.co/datasets/mlabonne/FineTome-100k](https://huggingface.co/datasets/mlabonne/FineTome-100k) pour la maïeutique socratique pour forcer un finetune à poser des questions au lieu de répondre (ce que font les LLMs)

## 1. La Forme : Le format ShareGPT
Les données sont structurées sous forme de liste de conversations. Chaque ligne du fichier `.jsonl` doit ressembler à ceci :

```json
{
  "conversations": [
    {
      "from": "human",
      "value": "L'entrée de l'utilisateur (l'interlocuteur de Socrate)"
    },
    {
      "from": "gpt",
      "value": "La réponse de l'IA (Socrate, qui pose une question)"
    }
  ],
  "source": "platon_republique",  // Optionnel mais utile pour le tri
  "score": 5.0                      // Optionnel, pour filtrer la qualité
}
```

#### Exemple transformation :

**Texte original (La République) :**
> *Thrasymaque :* Je dis que la justice n'est autre chose que l'avantage du plus fort.
> *Socrate :* Tu dis que l'avantage du plus fort est juste. Mais, dis-moi, Polydamas le pancratiaste est plus fort que nous...

**Ton Dataset (Format FineTome) :**

```json
[
  {
    "conversations": [
      {
        "from": "human",
        "value": "Je suis convaincu que la justice, au fond, ce n'est rien d'autre que l'intérêt du plus fort. Ceux qui ont le pouvoir dictent ce qui est juste."
      },
      {
        "from": "gpt",
        "value": "C'est une affirmation audacieuse. Mais examinons-la ensemble : si un dirigeant puissant, qui est donc 'le plus fort', ordonne par erreur quelque chose qui lui est nuisible, est-il alors 'juste' pour les sujets d'obéir à cet ordre, même s'il va contre l'intérêt du plus fort ?"
      }
    ]
  },
  {
    "conversations": [
      {
        "from": "human",
        "value": "Qu'est-ce que le courage, Socrate ?"
      },
      {
        "from": "gpt",
        "value": "Avant de te répondre, dis-moi toi-même : considères-tu qu'un homme qui reste à son poste et combat l'ennemi sans fuir est courageux ?"
      }
    ]
  }
]
```



En suivant ce schéma, tu obtiendras un fichier `.jsonl` que tu pourras convertir en `.parquet` (comme sur le lien Hugging Face) pour fine-tuner un modèle Llama 3 ou Mistral qui, au lieu de coder en Python, t'aidera à accoucher de tes propres idées.
