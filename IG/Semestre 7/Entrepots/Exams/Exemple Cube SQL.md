> [!important] Création de cube
> Création d'un cube avec un nombre de dimensions réduits rapport au sujet pour ne pas faire exploser Oracle
> On utilise des vues pour pouvoir utiliser des sub-queries, autrement impossible à utiliser (interdits dans les `GROUP BY`)
> A tester sur Oracle LiveSQL en créant les tables du sujet et en les remplissant après.
> Sujet : [[ENTR_EXAM_2017_2018.pdf]]

> Fait par un élève
> Les e.idE sont là pour bien aider à la compréhension mais sont à enlever pour la structure OLAP

```SQL
-- Vue pour les Informations sur les Enfants
CREATE VIEW Vue_Enfants AS
SELECT 
    e.idE,
    COUNT(enf.idE) AS nbr_enfants,
    MIN(EXTRACT(YEAR FROM SYSDATE) - EXTRACT(YEAR FROM enf.datenaissance)) AS age_min_enfant
FROM 
    Employe e
LEFT JOIN 
    Enfant enf ON enf.idE = e.idE
GROUP BY 
    e.idE;

-- Vue pour la Taille des Services
CREATE VIEW Vue_Taille_Service AS
SELECT 
    e.service,
    COUNT(e2.idE) AS taille_service
FROM 
    Employe e
JOIN 
    Employe e2 ON e2.service = e.service
GROUP BY 
    e.service;

-- Requête Principale avec GROUP BY CUBE
SELECT 
    e.idE,
    SUM(c.date_fin - c.date_debut) AS nbr_jour_conge, 
    EXTRACT(YEAR FROM SYSDATE) - EXTRACT(YEAR FROM e.datenaissance) AS age_employe,
    ve.nbr_enfants,
    ve.age_min_enfant,
    c.typeC
FROM 
    Employe e
JOIN 
    Conge c ON e.idE = c.idE
JOIN 
    Service s ON e.service = s.idS
LEFT JOIN 
    Vue_Enfants ve ON e.idE = ve.idE
JOIN 
    Vue_Taille_Service vts ON e.service = vts.service
GROUP BY 
    CUBE (
        e.idE, 
        EXTRACT(YEAR FROM SYSDATE) - EXTRACT(YEAR FROM e.datenaissance),
        ve.nbr_enfants,
        ve.age_min_enfant,
        c.typeC
    );
```