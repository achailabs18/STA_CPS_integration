.. SafeNet Trusted Access documentation master file, created by
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

===========================================================================================================================
Configurer SafeNet Trusted Access (STA) pour supporter les cartes CPS/CPE/CPA en tant que méthodes d'authentification forte
===========================================================================================================================

.. toctree::
   :maxdepth: 4
   :hidden:

Introduction
============

Cette documentation vous guidera à configurer SafeNet Trusted Access (STA) pour supporter les cartes CPS/CPE/CPA en tant que méthodes d'authentification forte permettant aux utilisateur d'accéder aux applications intégrées avec STA.

Prérequis
=========

- Un tenant SafeNet Trusted Access (STA) **Premium**
- **Cryptolib CPS** installé sur le poste de travail. **Cryptolib CPS** est un logiciel fourni par l'**Agence du Numérique en Santé** (**ANS**) qui permet l’interfaçage entre des applications informatiques et la carte CPS/CPE/CPA. Pour télécharger **Cryptolib CPS** :

  .. raw:: html
  
   <a href="https://esante.gouv.fr/services/espace-cps/telechargements-libres/cryptolib-cps-windows" target="_blank">https://esante.gouv.fr/services/espace-cps/telechargements-libres/cryptolib-cps-windows</a>


- Les utilisateurs des cartes CPS/CPE/CPA importés dans le tenant STA

  - soit manuellement via la console d'administrateur / SCIM API STA
  - soit automatiquement par l'agent de synchronisation LDAP

Configurer l'authentification par PKI côté STA
==============================================
1. Télécharger les certificats de l'autorité depuis le site IGC-Santé :

  - Pour les cartes de test:
  
   .. raw:: html
   
    <a href="http://igc-sante.esante.gouv.fr/AC%20TEST/Chaine_de_certification-IGC-Sante-TEST.p7b" target="_blank">http://igc-sante.esante.gouv.fr/AC%20TEST/Chaine_de_certification-IGC-Sante-TEST.p7b</a>

  - Pour les cartes de production:
  
   .. raw:: html
   
    <a href="http://igc-sante.esante.gouv.fr/AC/Chaine_de_certification-IGC-Sante.p7b" target="_blank">http://igc-sante.esante.gouv.fr/AC/Chaine_de_certification-IGC-Sante.p7b</a>

2. Extraire et sauvegarder les certificats

  a. Double-cliquer le fichier .p7b téléchargé dans l'étape précédent:
    .. thumbnail:: _images/CAp7b_1.PNG
    ..

  b. Sélectionner le certificat **AC IGC-SANTE ELEMENTAIRE PERSONNES** & **AC RACINE IGC-SANTE ELEMENTAIRE**. Puis cliquer **Action** > **All Tasks** > **Export...**:
      .. thumbnail:: _images/CertElementaire1.PNG
      ..

  c. Cliquer **Next** puis sélectionner l'option **PKCS #7 Certificates (.P7B)**:
      .. thumbnail:: _images/CertP7B.PNG
      ..

  d. Cliquer **Next** puis sélectionner l'endroit pour sauvegarder le fichier:
      .. thumbnail:: _images/CertElementaire2.PNG
      ..

  e. Cliquer **Next** puis **Finish**.

3. try something
