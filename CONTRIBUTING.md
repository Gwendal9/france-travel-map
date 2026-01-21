# 🤝 Contributing to France Travel Map

Merci de votre intérêt pour contribuer à ce projet !

## 🚀 Comment contribuer

### Signaler un bug

1. Vérifiez que le bug n'a pas déjà été signalé dans les [Issues](../../issues)
2. Créez une nouvelle issue avec le template "Bug Report"
3. Décrivez le bug de manière détaillée :
   - Comportement attendu
   - Comportement actuel
   - Étapes pour reproduire
   - Navigateur et version
   - Captures d'écran si possible

### Proposer une feature

1. Vérifiez la [Roadmap](README.md#roadmap) pour voir si la feature est déjà prévue
2. Créez une issue avec le template "Feature Request"
3. Décrivez :
   - Le problème que ça résout
   - La solution proposée
   - Des alternatives considérées

### Soumettre des modifications

1. **Fork** le projet
2. Créez une **branche** pour votre feature (`git checkout -b feature/AmazingFeature`)
3. **Testez** vos modifications dans plusieurs navigateurs
4. **Commitez** (`git commit -m 'Add some AmazingFeature'`)
5. **Push** vers la branche (`git push origin feature/AmazingFeature`)
6. Ouvrez une **Pull Request**

## 📝 Guidelines de code

### Style

- **React** : Utiliser les hooks (pas de classes)
- **Nommage** : camelCase pour variables/fonctions, PascalCase pour composants
- **Commentaires** : Documenter les fonctions complexes
- **Tailwind** : Préférer Tailwind aux CSS custom

### Structure

```javascript
// ✅ Bon
function MyComponent({ prop1, prop2 }) {
  const [state, setState] = useState(initialValue);
  
  useEffect(() => {
    // Effect logic
  }, [dependencies]);
  
  const handleClick = () => {
    // Handler logic
  };
  
  return (
    <div className="tailwind-classes">
      {/* JSX */}
    </div>
  );
}

// ❌ Éviter
class MyComponent extends React.Component {
  // Classes non utilisées dans ce projet
}
```

### Performance

- Utiliser `useMemo` pour calculs coûteux
- Utiliser `useCallback` pour fonctions passées en props
- Éviter les re-renders inutiles

### Tests

Avant de soumettre :
- [ ] Tester dans Chrome
- [ ] Tester dans Firefox
- [ ] Tester sur mobile (responsive)
- [ ] Vérifier que localStorage fonctionne
- [ ] Pas d'erreurs dans la console

## 🎨 Bonnes pratiques

### Commits

Format : `type(scope): message`

Types :
- `feat`: Nouvelle feature
- `fix`: Correction de bug
- `docs`: Documentation
- `style`: Formatting, CSS
- `refactor`: Refactoring
- `perf`: Performance
- `test`: Tests
- `chore`: Maintenance

Exemples :
```
feat(map): add photo gallery
fix(modal): correct city placement algorithm
docs(readme): update installation instructions
style(css): improve map texture
```

### Pull Requests

Titre : Résumé clair de la modification

Description :
- **Quoi** : Ce qui a été changé
- **Pourquoi** : Raison de la modification
- **Comment** : Approche technique (si pertinent)
- **Tests** : Comment tester
- **Screenshots** : Si changements visuels

## 🐛 Debugging

### Console logs

```javascript
// Pour debug seulement, à retirer avant commit
console.log('Debug:', value);

// Préférer
if (process.env.NODE_ENV === 'development') {
  console.log('Debug:', value);
}
```

### localStorage

```javascript
// Vérifier les données
console.log(JSON.parse(localStorage.getItem('franceMapStateV2')));

// Réinitialiser si besoin
localStorage.clear();
```

## 📚 Ressources

- [React Documentation](https://react.dev)
- [Tailwind CSS](https://tailwindcss.com)
- [GeoJSON Specification](https://geojson.org)
- [SVG Path Tutorial](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths)

## ❓ Questions

Pour toute question, n'hésitez pas à :
- Ouvrir une issue
- Consulter la [documentation](README.md)
- Rejoindre les discussions

Merci de contribuer ! 🎉
