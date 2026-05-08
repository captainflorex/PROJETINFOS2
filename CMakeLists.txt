cmake_minimum_required(VERSION 3.10)
project(Projet_INFO_SEM2 C)

set(CMAKE_C_STANDARD 99)

add_executable(Projet_INFO_SEM2
        main.c
        affichage.c
        jeu.c
        entrees.c
        menu.c
        sauvegarde.c
        eclair.c
)

# Includes alfont
target_include_directories(Projet_INFO_SEM2 PRIVATE
        ${CMAKE_SOURCE_DIR}/alfont-code-r12-trunk/alfont-code-r12-trunk/include
)

# Lib alfont compilée
target_link_libraries(Projet_INFO_SEM2
        ${CMAKE_SOURCE_DIR}/alfont-code-r12-trunk/alfont-code-r12-trunk/lib/mingw32/libalfont.a
        -lmingw32
        -lalleg44
        -lm
)

# --- Section Doxygen ---

# 1. Chercher si Doxygen est installé
find_package(Doxygen)

if (DOXYGEN_FOUND)
    # 2. Configurer les options de Doxygen (optionnel mais recommandé)
    set(DOXYGEN_PROJECT_NAME "Documentation ${PROJECT_NAME}")
    set(DOXYGEN_GENERATE_HTML YES)
    set(DOXYGEN_GENERATE_LATEX NO) # Désactivé pour gagner du temps
    
    # 3. Créer la commande pour générer la doc
    # Cela crée une cible nommée "doc"
    doxygen_add_docs(doc
        ${CMAKE_CURRENT_SOURCE_DIR}
        COMMENT "Génération de la documentation avec Doxygen"
    )
else()
    message(WARNING "Doxygen n'a pas été trouvé. La cible 'doc' ne sera pas créée.")
endif()

