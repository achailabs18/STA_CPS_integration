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

Cette documentation vous guidera à configurer **SafeNet Trusted Access (STA)** pour supporter les **cartes CPS/CPE/CPA** en tant que méthodes d'authentification fortes.

Prérequis
=========

- Un tenant **SafeNet Trusted Access (STA) Premium**
- **Cryptolib CPS** installé sur le poste de travail d'utilisateur. **Cryptolib CPS** est un logiciel fourni par l'**Agence du Numérique en Santé** (**ANS**) qui permet l’interfaçage entre des applications informatiques et les cartes CPS/CPE/CPA. Pour télécharger **Cryptolib CPS** : https://esante.gouv.fr/services/espace-cps/telechargements-libres/cryptolib-cps-windows
- Les utilisateurs des cartes CPS/CPE/CPA importés dans le tenant STA

  - soit manuellement via la console d'administrateur
  - soit automatiquement

    - par l'agent de synchronisation LDAP.
    - par les APIs SCIM/REST.

  Pour plus d'information : https://www.thalesdocs.com/sta/Content/STA/Users/AddUsrs.htm

- Les numéros d'**Identification Nationale du PS** de ces utilisateurs doivent également être renseignés dans le référentiel d'utilisateurs STA. Si ces numéros sont présents dans le référentiel de l'établissement de santé, ils peuvent aussi être synchronisés vers les champs Alias / Custom Field des comptes d'utilisateur STA.

  - Pour info, ces numéros d'**Identification Nationale du PS** correspondent aux données **PS_IdNat** définies dans la documentation ANS suivante : https://esante.gouv.fr/sites/default/files/media_entity/documents/ci-sis_anx_sources-donnees-professionnels-structures_v1.5_0.pdf (voir la section "5.4.  PS_IdNat", P.20 - 21)
  - Ce numéro est donc une contatenation du **type d’identifiant** (0 à 9) et de l’**identifiant national**
  - Par ex., un médecin ayant un numéro RPPS aurait le numéro suivant : 801234567890
  - Ce numéro se trouvent également dans l'attribut **CN** du champ **Subject** du certificat de l'utilisateur. Par ex. :
  .. thumbnail:: _images/CertUser1.png
    :width: 300px
  ..


Configurer l'authentification par certificat dans STA
=====================================================
1. Télécharger & sauvegarder les certificats d'autorité depuis le site IGC-Santé
--------------------------------------------------------------------------------

  - Pour les cartes de test : http://igc-sante.esante.gouv.fr/AC%20TEST/Chaine_de_certification-IGC-Sante-TEST.p7b
  - Pour les cartes de production : http://igc-sante.esante.gouv.fr/AC/Chaine_de_certification-IGC-Sante.p7b

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

  b. Sélectionner le certificat **AC IGC-SANTE STANDARD PERSONNES** & **AC RACINE IGC-SANTE STANDARD**. Puis cliquer **Action** > **All Tasks** > **Export…** :
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
---------------------------------------------
  a. Double-cliquer le fichier .p7b téléchargé dans l'étape 1 :

  b. Sélectionner le certificat **AC IGC-SANTE FORT PERSONNES** & **AC RACINE IGC-SANTE FORT**. Puis cliquer **Action** > **All Tasks** > **Export…** :
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
  a. Connectez-vous à la console d'administrateur STA : https://sta.eu.safenetid.com

  b. Cliquer sur l'icône **Settings** puis cliquer **Certificate-based Authentication** > **Add Issuing CA** :
    .. thumbnail:: _images/STA_CBA1.png
      :width: 300px
    ..

  c. Sélectionner le fichier .p7b (**ELEMENTAIRE**) généré dans l'étape 2.

  d. Sélectionner **Email address** comme **CERTIFICATE ATTRIBUTE** & **USER ATTRIBUTE** dans **User Mapping** > **Save** :
    .. thumbnail:: _images/STA_CBA2.png
      :width: 300px
    ..

  e. Répéter les étapes **a** à **d** pour les certificats d'autorité **STANDARD** (l'étape 3) & **FORT** (l'étape 4).

6. Créer une politique d'accès avec l'authentification par certificat
---------------------------------------------------------------------
Nous allons créer une politique d'accès avec l'authentification par certificat (**cartes CPS/CPE/CPA**) activée. Dans cet exemple, nous allons activier cette méthode d'authentification pour le portail d'utilisateur STA pour tous les utilisateurs du tenant.

  a. Cliquer sur l'icône **Policies** puis ajouter une nouvelle politique d'accès en cliquant sur **+** :
    .. thumbnail:: _images/STA_CBA3.png
      :width: 300px
    ..

  b. Renseigner les détails de la nouvelle politique d'accès :
    - Donner un nom ("Cartes CPS CPE CPA" par ex.)
    - Sélectionner "All users"
    - Sélectionner l'application "User Portal"
    - Sélectionner la méthode "Certificate-Based Authentication (CBA)"
    - Sélectionner "Every access attempt"

      .. thumbnail:: _images/STA_CBA4.png
        :width: 300px
      ..

  c. **Save**

Tester l'authentification avec une carte CPS/CPE/CPA
====================================================
Nous allons donc tester l'authentification au portail d'utilisateur STA avec une carte CPS/CPE/CPA.

  a. Récupérer le lien du portail d'utilisateur STA
    - Cliquer sur l'icône **Applications** > **User Portal** > Copier l'URL en cliquant sur le bouton **Copy**.

      .. thumbnail:: _images/STA_CBA5.png
        :width: 300px
      ..

  b. Ouvrir un nouvel onglet ou un navigateur web et connectez-vous à l'URL du portail d'utilisateur.
  c. Insérer la carte CPS/CPE/CPA dans un lecteur connecté au poste de travail.
  d. Saisir le nom d'utilisateur puis **LOGIN**.
  e. Saisir le code PIN de la carte puis **OK**.
