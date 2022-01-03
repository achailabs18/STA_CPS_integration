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

Cette documentation vous guidera à configurer **SafeNet Trusted Access (STA)** pour supporter les **cartes CPS/CPE/CPA** en tant que méthodes d'authentification forte.

Prérequis
=========

- Un tenant SafeNet Trusted Access (STA) **Premium**
- **Cryptolib CPS** installé sur le poste de travail. **Cryptolib CPS** est un logiciel fourni par l'**Agence du Numérique en Santé** (**ANS**) qui permet l’interfaçage entre des applications informatiques et les cartes CPS/CPE/CPA. Pour télécharger **Cryptolib CPS** :

  .. raw:: html

   <a href="https://esante.gouv.fr/services/espace-cps/telechargements-libres/cryptolib-cps-windows" target="_blank">https://esante.gouv.fr/services/espace-cps/telechargements-libres/cryptolib-cps-windows</a>

..
- Les utilisateurs des cartes CPS/CPE/CPA importés dans le tenant STA

  - soit manuellement via la console d'administrateur
  - soit automatiquement

    - par l'agent de synchronisation LDAP
    - par les APIs SCIM/SOAP

Configurer l'authentification par PKI côté STA
==============================================
1. Télécharger les certificats de l'autorité depuis le site IGC-Santé
---------------------------------------------------------------------

  - Pour les cartes de test :
  
   .. raw:: html
   
    <a href="http://igc-sante.esante.gouv.fr/AC%20TEST/Chaine_de_certification-IGC-Sante-TEST.p7b" target="_blank">http://igc-sante.esante.gouv.fr/AC%20TEST/Chaine_de_certification-IGC-Sante-TEST.p7b</a>

  - Pour les cartes de production :
  
   .. raw:: html
   
    <a href="http://igc-sante.esante.gouv.fr/AC/Chaine_de_certification-IGC-Sante.p7b" target="_blank">http://igc-sante.esante.gouv.fr/AC/Chaine_de_certification-IGC-Sante.p7b</a>

2. Extraire et sauvegarder le certificat ELEMENTAIRE
----------------------------------------------------
  a. Double-cliquer le fichier .p7b téléchargé dans l'étape 1 :

  b. Sélectionner le certificat **AC IGC-SANTE ELEMENTAIRE PERSONNES** & **AC RACINE IGC-SANTE ELEMENTAIRE**. Puis cliquer **Action** > **All Tasks** > **Export…** :
    .. thumbnail:: _images/CertElementaire1.png
    ..

  c. Cliquer **Next** puis sélectionner l'option **PKCS #7 Certificates (.P7B)** :
    .. thumbnail:: _images/CertP7B.png
      :width: 300px
    ..

  d. Cliquer **Next** puis sélectionner l'endroit pour sauvegarder le fichier :
    .. thumbnail:: _images/CertElementaire2.png
      :width: 300px
    ..

  e. Cliquer **Next** puis **Finish**.

3. Extraire et sauvegarder le certificat STANDARD
-------------------------------------------------
  a. Double-cliquer le fichier .p7b téléchargé dans l'étape 1 :

  b. Sélectionner le certificat **AC IGC-SANTE ELEMENTAIRE STANDARD** & **AC RACINE IGC-SANTE STANDARD**. Puis cliquer **Action** > **All Tasks** > **Export…** :
    .. thumbnail:: _images/CertStandard1.png
    ..

  c. Cliquer **Next** puis sélectionner l'option **PKCS #7 Certificates (.P7B)** :
    .. thumbnail:: _images/CertP7B.png
      :width: 300px
    ..

  d. Cliquer **Next** puis sélectionner l'endroit pour sauvegarder le fichier :
    .. thumbnail:: _images/CertStandard2.png
      :width: 300px
    ..

  e. Cliquer **Next** puis **Finish**.

4. Extraire et sauvegarder le certificat FORT

  a. Double-cliquer le fichier .p7b téléchargé dans l'étape 1 :

  b. Sélectionner le certificat **AC IGC-SANTE ELEMENTAIRE FORT** & **AC RACINE IGC-SANTE FORT**. Puis cliquer **Action** > **All Tasks** > **Export…** :
    .. thumbnail:: _images/CertFort1.png
    ..

  c. Cliquer **Next** puis sélectionner l'option **PKCS #7 Certificates (.P7B)** :
    .. thumbnail:: _images/CertP7B.png
      :width: 300px
    ..

  d. Cliquer **Next** puis sélectionner l'endroit pour sauvegarder le fichier :
    .. thumbnail:: _images/CertFort2.png
      :width: 300px
    ..

  e. Cliquer **Next** puis **Finish**.

5. Importer les certificats de l'autorité IGC-Santé dans STA
------------------------------------------------------------
  a. Connectez-vous à la console d'administrateur STA :
   .. raw:: html
   
    <a href="https://sta.eu.safenetid.com" target="_blank">https://sta.eu.safenetid.com</a>

  b. Cliquer sur l'icône **Settings** puis cliquer **Certificate-based Authentication** > **Add Issuing CA** :
    .. thumbnail:: _images/STA_CBA1.png
      :width: 300px
    ..

  c. Sélectionner le fichier .p7b (**ELEMENTAIRE**) généré dans l'étape 2.

  d. Sélectionner **Email address** comme **USER ATTRIBUTE** dans **User Mapping** > **Save** :
    .. thumbnail:: _images/STA_CBA2.png
      :width: 300px
    ..

  e. Répéter les étapes **a** à **d** pour les certificats de l'autorité **STANDARD** & **FORT**.
