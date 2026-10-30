---
title: 'Intégrer Supabase au projet Next.js'
type: 'feature'
created: '2026-10-30'
status: 'done'
route: 'oneshot'
review_loop_iteration: 0
context: []
---

<frozen-after-approval reason="human-owned intent — do not modify unless human renegotiates">

## Intent

**Problem:** Le projet Next.js n’a pas encore de connexion configurée à l’instance Supabase fournie par l’utilisateur.

**Approach:** Ajouter les SDK et utilitaires de client navigateur/serveur adaptés à Next.js, configurer les identifiants publics fournis en local, et préparer le rafraîchissement des sessions Auth côté serveur.

</frozen-after-approval>

## Implementation Notes

- Ajout des SDK `@supabase/ssr` et `@supabase/supabase-js`, avec des clients navigateur et serveur dans `src/lib/supabase/`.
- Configuration locale des variables `NEXT_PUBLIC_SUPABASE_URL` et `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY` avec l’URL et la clé publiable fournies; `.env.local` reste ignoré par Git. Ajout de `proxy.ts` pour le rafraîchissement des sessions Auth, sans contrôle d’accès automatique.
- Documentation des variables et de l’usage dans `README.md`.

## Review Triage Log

- `low` — Le README ne nommait pas les variables ni la source des valeurs; les noms et les paramètres du tableau de bord Supabase sont documentés.
- `low` — Le README n’indiquait pas qu’un changement d’environnement demande un redémarrage du serveur; cette étape est ajoutée.
- `medium` — Le comportement de `setAll` dans un Server Component pouvait prêter à confusion; la documentation précise que les écritures de cookies se font dans les Server Actions et Route Handlers.
- `medium` — Le proxy pouvait être interprété comme un contrôle d’accès; le README précise qu’il ne fait que rafraîchir les sessions et rappelle les claims et RLS.
- `low` — L’absence de configuration ne disait pas clairement son effet; le README indique que les helpers échouent avec une erreur de configuration.
- `low` — La gestion des erreurs Supabase n’était pas mentionnée; le README signale le champ `error` à traiter par les appelants.
- `low` — Les notes de spécification ne nommaient pas les variables ni le caractère publiable de la clé; elles les identifient maintenant explicitement.
- `false` — Le statut `in-progress` était normal pendant l’implémentation et le workflow one-shot omet les critères d’acceptation; la spécification est finalisée en `done`.
- `low` — Le matcher pouvait traiter quelques extensions d’assets statiques; les extensions d’icônes, polices, CSS, JavaScript et manifestes sont désormais exclues.
- `false` — Le matcher couvre volontairement les routes `/api` pour maintenir le rafraîchissement des sessions; ce comportement est maintenant documenté et le matcher peut être resserré si une route future le nécessite.

