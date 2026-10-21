LA ROSA — Menu public + dashboard admin connecté à Supabase

FICHIERS
- index.html : menu public en lecture seule (aucun lien Dashboard)
- dashboard.html : administration avec connexion email/mot de passe
- config.js : URL Supabase et clé anon/publishable
- supabase_schema.sql : tables et politiques de sécurité RLS

MISE EN PLACE (nécessite un projet Supabase)
1. Crée un projet Supabase.
2. Ouvre SQL Editor et exécute supabase_schema.sql.
3. Dans Authentication > Users, crée ton compte administrateur (email + mot de passe).
4. Copie l'UUID du compte. Dans SQL Editor, exécute :
   insert into public.admin_users (user_id) values ('UUID-DU-COMPTE');
5. Dans Project Settings > API, copie Project URL et la clé anon/publishable.
6. Colle-les dans config.js (les clés publiques anon/publishable sont prévues pour le navigateur; ne jamais mettre service_role).
7. Héberge les fichiers ensemble sur un hébergeur statique HTTPS (Netlify, Vercel, GitHub Pages, etc.).
8. Visite index.html pour le menu client. Visite dashboard.html pour te connecter et gérer le menu.

IMPORTANT
- Le menu public n'a aucun bouton ou lien vers le dashboard.
- La vraie protection est assurée côté base par les politiques RLS : seuls les user_id présents dans admin_users peuvent écrire.
- Les fichiers doivent être servis depuis un site web (localhost/HTTPS) pour un fonctionnement fiable, pas seulement ouverts en file://.
- Le dashboard modifie les tables partagées; les changements apparaissent lors du prochain chargement du menu public.
- Ce bundle ne peut pas créer ton projet Supabase ni publier le site à ta place. Tu dois renseigner les identifiants de ton propre projet.
