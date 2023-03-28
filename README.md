# I - Workbox:

## Lite des fonctionnalitées:

- Generer des services worker et manifest
- Faciliter la mise en cache des éléments du site (css, réponse de requêtes...). Et donne la possibilité de donner des zone de cache et des temps d'expiration de cache.

## Méthodes de cache et utilisations possibles

Plusieurs méthodes : 
- networkFirst :regarde le réseaux en premier puis le cache. (dans le cas de page dynamiques)
- cacheFirst :regarde le cache en premier puis le réseaux. (dans le cas de page qui ne change pas beacoup)
- cacheOnly :regarde uniquement le cache (ok si nous avons un acces limité à internet ou si la batterie est faible)
- networkOnly: regarde uniquement le réseau (je ne vois pas l'interet, parceque pas de cache)
- staleWhileRevalidate: demande aux deux en même temps, affichera donc le cache puis le réseaux, est interressant si on doit avoir une application avec un affichage tres "rapide"

## Uses cases à intégrer dans le projet doctoliberal

Alors, je n'ai pas fais le cas de doctoliberal, mais pour l'application de barkeeper's assistant :
En ce qui concerne la génération de manifest, elle aurait pu être faite avec workbox.

On pourrait utiliser le staleWhileRevalidate pour tout le rapport de la table : si c'est la même personne qui a prit les commandes avant, la device aura en cache les infos initiales, donc l'historique ne devrait pas changer et l'affichage sera plus rapide.
Pour ce qui concerne le menu, on serait en cacheFirst, car les plat et les prix ne sont pas censer changer dans la soirée, il suffit de mettre un temps de rafraichissement de 1 heures et on devrait être bon.
Pour le payment en revanche, il sera obligatoire d'être en networkFirst car on ne veut pas commencer à donner un mauvais prix au client.

 
# II - Page d'incitation à l'installation de PWA
 
## 1 ) Créer un composant (React / Vue / angular / HTML+CSS) pour inciter et surtout guider un utilisateur à installer la PWA

Alors, je vais simplement partir du principe que ce que j'ai fait pour le projet peut être copier coller :

```TypeScript
'use client';
import Link from "next/link";
import Image from 'next/image'

export default function Pwa() {
  return (
    <>      
      <section className="bg-gray-50 dark:bg-gray-900">
        <div className="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0">
          <div className="w-full bg-white rounded-lg shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700">
            <div className="p-6 space-y-4 md:space-y-6 sm:p-8">
              <h1 className="text-xl font-bold leading-tight tracking-tight text-gray-900 md:text-2xl dark:text-white">
                La PWA qu'est ce que c'est ?
              </h1>
              <div className="w-full dark:text-white">   
                <p>
                  La PWA ou Progressive Web Application est ce qui va permettre d'installer votre application sur votre appareil pour pouvoir simplement avoir un raccourci sur votre bureau sur ordinateur, mais surtout pour avoir l'application sur vos mobiles et tablettes.
                  une fois l'application installer vous pourrez profiter de fonctionnalité que vous n'aviez pas sur le site : utilisation nfc, vibrations, notifications push etc ...
                </p>
                <p>
                  Les PWA peuvent être accessibles depuis n'importe quel navigateur de smartphone, que ce soit sur Android ou IOS.
                </p>
                <p>
                  Comment l'installer ? il suffit de cliquer sur cette icone dans la barre d'URL du site : 
                </p>
                <Image src="/images/pwa.PNG" alt="Image de l'icone dans la barre d'URL" 
                  width={10000}
                  height={30}
                  />
              </div>  
              <a href="mailto:barkeeperSupport@gmail.com?subject=Problème sur la page pwa&body=Veuillez expliquer le problème et fournir un scénario dans le corps du mail">Signaler un problème</a>                
            </div>
          </div>
        </div>
      </section>
    </>
  )
}
```
les classes sont issues de Tailwind, je mettrais l'image dans le repo git


## 2 ) Expliquer en quoi il serait interessant de mettre en place une telle page

L'interet de mettre cette page est de permettres d'informer les utilisateurs de la possibilité d'obtenir l'application de leur site, cela aura plusieurs effets : Les utilisateurs seront plus apte a télécharger l'application, ce qui induit que les fonctionnalitées que l'on a apportés à la PWA seront utilisées, et rendra leur experience plus aggréable. De plus une fois la PWA téléchargée, il est plus tentant d'aller sur l'application que de repasser par un navigateur (plus facile d'acces, pas besoin de retapper l'adresse / rechercher le site sur internet)

