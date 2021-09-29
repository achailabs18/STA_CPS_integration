.. SafeNet Trusted Access documentation master file, created by
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

===========================================================================================================================
Configurer SafeNet Trusted Access (STA) pour supporter les cartes CPS/CPE/CPA en tant que méthodes d'authentification forte
===========================================================================================================================

.. toctree::
   :maxdepth: 3
   :hidden:

Introduction
============

Cette documentation vous guidera à configurer SafeNet Trusted Access (STA) pour supporter les cartes CPS/CPE/CPA en tant que méthodes d'authentification forte permettant aux utilisateur d'accéder aux applications intégrées avec STA.

Prérequis
=========

  - Un tenant SafeNet Trusted Access (STA) **Premium**
  - **Cryptolib CPS** installé sur le poste de travail. **Cryptolib CPS** est un logiciel fourni par l'**Agence du Numérique en Santé** (**ANS**) qui permet l’interfaçage entre des applications informatiques et la carte CPS/CPE/CPA. Pour télécharger **Cryptolib CPS**:

   .. raw:: html
   
    <a href="https://esante.gouv.fr/services/espace-cps/telechargements-libres/cryptolib-cps-windows" target="_blank">https://esante.gouv.fr/services/espace-cps/telechargements-libres/cryptolib-cps-windows</a>


  - Les utilisateurs des cartes CPS/CPE/CPA importés dans le tenant STA
     - soit manuellement via la console d'administrateur / SCIM API STA
     - soit automatiquement par l'agent de synchronisation LDAP


