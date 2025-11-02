# EYC_REVI

# (# ============================================================
# 🎓 UNIVERSITÉ DE BOURGOGNE – TD Social Listening
# Extraction complète des commentaires YouTube (avec réponses)
# ============================================================

"""
📘 Présentation :
Ce script permet d’extraire tous les commentaires d’une vidéo YouTube,
ainsi que les réponses associées, en utilisant l’API officielle de YouTube Data v3.

⚠️ LIMITES IMPORTANTES DE L’API YOUTUBE :
------------------------------------------
1️⃣ L’API ne renvoie jamais plus de 100 résultats par requête.
   → Le script gère cela automatiquement grâce au paramètre 'nextPageToken'.

2️⃣ Certaines réponses ne sont **pas accessibles** :
   - si elles sont modérées, supprimées, ou en “replies à une réponse” (niveau 2+)
   - ou si le créateur de la vidéo a activé un filtrage.
   → Dans ce cas, l’API affiche bien un `totalReplyCount`, mais renvoie 0 éléments.

3️⃣ `maxResults` > 100 est ignoré silencieusement.
   → Mettre une valeur plus haute ne provoque pas d’erreur, mais n’a aucun effet.

Le script contourne ces limites en :
- récupérant les données page par page (jusqu’à épuisement de 'nextPageToken'),
- respectant les délais pour ne pas dépasser les quotas (via time.sleep),
- distinguant les commentaires principaux ("top") et les réponses ("reply").

Auteur : ChatGPT (version pédagogique adaptée pour TD)
Encadrant : Université de Bourgogne – Master Social Listening
