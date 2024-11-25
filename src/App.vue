
<template>
  <div id="app" class="digital-museum">
    <div class="hide">
      <h4>Sorry, this musuem is not accessible to your device. Open it on bigger devices. 1280px above.</h4>
    </div>
    <!-- Header Section -->
    <section class="museum-header">
      <h1>Welcome to Ocho-ocho Digital Museum</h1>
      <div class="h-description">
        <p>
          Discover the vibrant heart of Philippine popular culture. Our digital
          museum celebrates iconic moments, cherished stories, and timeless
          creativity that define our shared identity. Explore and relive the
          spirit of the Filipinos.
        </p>
      </div>
      <button class="header-btn" @click="scrollToNextSectionFromHeader">
        <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" fill="currentColor" class="bi bi-chevron-double-down" viewBox="0 0 16 16">
          <path fill-rule="evenodd" d="M1.646 6.646a.5.5 0 0 1 .708 0L8 12.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708"/>
          <path fill-rule="evenodd" d="M1.646 2.646a.5.5 0 0 1 .708 0L8 8.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708"/>
        </svg>
      </button>
    </section>

    <!-- Main Title Section -->
    <section id="group-section" class="group-section">
      <div class="group-name">
          <h1>{{ groupName }}</h1>
          </div>
          <div class="group-members">
            <span v-for="(member, index) in groupMembers" :key="index">
              {{ member }}
            </span>
          </div>
    </section>

        <!-- Content Sections -->
        <section class="sections-container">
          <div
            rel="preload"
            v-for="(section, sectionIndex) in sections"
            :key="sectionIndex"
            class="museum-section"
            :style="{
              ...getBackgroundStyle(sectionIndex),
              minHeight: '100vh',
            }"
          >
            <div>
              <h3>{{ section.title }}</h3> 
              <span class="intro">{{ section.intro }}</span>
            </div>
            <div class="subsections">
              <div
                rel="preload"
                v-for="(subsection, subsectionIndex) in section.subsections"
                :key="subsectionIndex"
                class="subsection"
                :style="{ backgroundImage: `url(${coverImage})` }"
                @click="openVirtualRoom(sectionIndex, subsectionIndex)"
              >
                <div class="subsection-title">{{ subsection.title }}</div>
                <button @click="openVirtualRoom(sectionIndex, subsectionIndex)">
                  Check Out Room
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    width="30"
                    height="30"
                    fill="currentColor"
                    class="bi bi-arrow-right-short"
                    viewBox="0 0 16 16"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M4 8a.5.5 0 0 1 .5-.5h5.793L8.146 5.354a.5.5 0 1 1 .708-.708l3 3a.5.5 0 0 1 0 .708l-3 3a.5.5 0 0 1-.708-.708L10.293 8.5H4.5A.5.5 0 0 1 4 8"
                    />
                  </svg>
                </button>
              </div>
            </div>
            <div>
              <div>
              <div class="subintro"><p>{{ section.subintro }}</p></div>
            </div>
            </div>
      </div>
    </section>

    <!-- References -->
    <section class="reference-container">
      <div>
        <h5>{{ title_white }}</h5>
        <ul class="reference-wrapper">
                <li v-for="(ref, index) in references" :key="index">
                  {{ ref }}
                </li>
          </ul>
      </div>
    </section>

    <!-- Closing -->
    <section class="closing">
      <h1>Thank you for visiting Ocho-ocho Digital Museum</h1>
    </section>

    <!-- Virtual Room Modal -->
    <div v-if="showModal" class="modal-overlay" @click.self="closeVirtualRoom">
      <div class="modal-content">
        <h3>{{ activeRoom.subtitle }}</h3>
        <p class="description">{{ activeRoom.description }}</p>
        <div class="images-container">
          <img
            rel="preload"
            v-for="(image, index) in activeRoom.images"
            :key="index"
            :src="image"
            alt="Subsection image"
            class="modal-image"
          />
        </div>
        <button class="close-modal" @click="closeVirtualRoom">Close</button>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      coverImage: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732493493/Teambangan%20Museum/BG%20Covers/cover_v9nd2b.png',
      groupName: "Built and Presented by Teambangan",
      groupMembers: [
        "Jhan Philippe Moloa",
        "Maycaela Enguito",
        "Jether Daniel Torres",
      ],
      title_white: "References",
      references: [
            "Rossen, J. (2018, September 13). Antisocial media: the rise and fall of Friendster. Mental Floss. https://www.mentalfloss.com/article/556413/friendster-rise-and-fall-jonathan-abrams?utm_source=chatgpt.com",
            "Wikipedia contributors. (2024, October 30). Friendster. Wikipedia. https://en.wikipedia.org/wiki/Friendster?utm_source=chatgpt.com",
            "Natividad, N. (2015, July 2). A history of the BPO industry in numbers. RAPPLER. https://www.rappler.com/brandrap/profiles-and-advocacies/98207-bpo-philippines-timeline/?utm_source=chatgpt.com",
            "Mercado, L. (2024, October 9). History of outsourcing in the Philippines. Outsource Philippines. https://outsource-philippines.com/the-history-of-outsourcing-in-the-philippines-key-milestones-and-growth/?utm_source=chatgpt.com",
            "The Philippines: Extremism and Terrorism. (n.d.). The Counter Extremism Project. Retrieved November 23, 2024, from https://www.counterextremism.com/countries/philippines-extremism-and-terrorism?",
            "Brey, J. (2023). Terrorism in the Philippines: Persistent threat and effective response. Contemporary Issues in Air and Space Power, 1(1), bp33148316. https://doi.org/10.58930/bp33148316",
            "Republic Act No. 10066. (n.d.-b). https://lawphil.net/statutes/repacts/ra2010/ra_10066_2010.html?",
            "Wikipedia contributors. (2024b, November 20). Typhoon Ketsana. Wikipedia. https://en.wikipedia.org/wiki/Typhoon_Ketsana",
            "Global Facility for Disaster Reduction and Recovery (GFDRR). (n.d.). Philippines- 2009- Typhoons Ondoy and Pepeng affected 9.3 million people | GFDRR. www.gfdrr.org. https://www.gfdrr.org/en/philippines-2009-typhoons-ondoy-and-pepeng-affected-93-million-people",
            "National Disaster Coordinating Council (NDCC). (2010, September 27). Philippines: NDCC UPDATE - Final Report on Tropical Storm “ONDOY” and Typhoon “PEPENG” - Philippines | ReliefWeb. Reliefweb.int. https://reliefweb.int/report/philippines/philippines-ndcc-update-final-report-tropical-storm-ondoy-and-typhoon-pepeng",
            "United Nations Office for the Coordination of Humanitarian Affairs. (2024). Ketsana Reports. Unocha.org. https://www.unocha.org/results?q=ketsana#gsc.tab=0&gsc.q=ketsana&gsc.page=1",
            "Lagare, J. B. (2024, October 14). PH remains world's largest rice importer. INQUIRER.net. https://business.inquirer.net/484774/ph-remains-worlds-largest-rice-importer",
            "Wikipedia contributors. (2024e, November 21). Philippine drug war. Wikipedia. https://en.wikipedia.org/wiki/Philippine_drug_war",
            "Vlacano. (2021, December 9). YouTube FanFest 2021: A three-day celebration of Filipino talent and diversity. POP! https://pop.inquirer.net/115198/youtube-fanfest-2021-a-three-day-celebration-of-filipino-talent-and-diversity",
            "Wikipedia contributors. (2024d, November 22). Tropical Storm Trami (2024). Wikipedia. https://en.wikipedia.org/wiki/Tropical_Storm_Trami_(2024)",
            "Suciu, P. (2023, November 10). How Elon Musk changed Twitter a year and $44 billion later. Forbes. https://www.forbes.com/sites/petersuciu/2023/11/08/twitter-has-changed-a-lot-since-elon-musk-bought-it-a-year-ago/",
            "Wikipedia contributors. (2024, November 11). Precious Lara Quigaman. Wikipedia. https://en.wikipedia.org/wiki/Precious_Lara_Quigaman",
            "Wikipedia contributors. (2024b, November 18). Marian Rivera. Wikipedia. https://en.wikipedia.org/wiki/Marian_Rivera",
            "Wikipedia contributors. (2024a, November 5). Emo subculture. Wikipedia. https://en.wikipedia.org/wiki/Emo_subculture",
            "A brief history of hobby and fandom conventions in the Philippines. (n.d.). https://charles-tan.blogspot.com/2007/10/brief-history-of-hobby-and-fandom.html",
            "Serrano, C. J., Conda, C., III, Cruz, J. E., & Guzman, G. K. (2022). “What's Wrong with One More Episode?”: Why Korean Dramas are a Hit in the Philippines. DLSU SHS Research Congress. https://animorepository.dlsu.edu.ph/cgi/viewcontent.cgi?article=1007&context=conf_shsrescon",
            "Arroyo, A., Chong, E., Concha, G., & Sy, F. (2023). The Negative Effects of TikTok To The Body Image of The Grade 12 DLSU-Taft Female Students. DLSU SHS Research Congress, 5th. https://animorepository.dlsu.edu.ph/cgi/viewcontent.cgi?article=1761&context=conf_shsrescon",
            "Prieler, Michael & Centeno, Dave. (2013). Gender Representation in Philippine Television Advertisements. Sex Roles. 69. 10.1007/s11199-013-0301-4. https://www.researchgate.net/publication/257663762_Gender_Representation_in_Philippine_Television_Advertisements",
            "Mercado, M. (2022, January 6). Skin lightening in Manila: body confidence or body colonialism? Medium. https://medium.com/writ-150-at-usc-fall-2020/skin-lightening-in-manila-body-confidence-or-body-colonialism-f916a6eef189",
            "Adorable, G. (2021). Cosmetic Surgery and Media: Contributing to Filipino women's beauty ideals and Self-Esteem. Pup. https://www.academia.edu/23184322/Cosmetic_Surgery_and_Media_Contributing_to_Filipino_Women_s_Beauty_Ideals_and_Self_Esteem",
            "Corpuz, A. (n.d.). Impact of Korean-Pop on the beauty standards of young Filipinos. Scribd. https://www.scribd.com/document/652993588/Impact-of-Korean-Pop-on-the-Beauty-Standards-of-Young-Filipinos",
            "The Metaverse is here: Virtual reality's leap toward connecting worlds. (n.d.). The Benildean. https://read.thebenildean.org/2023/01/the-metaverse-is-here-virtual-realitys-leap-toward-connecting-worlds",
            "DOST-PCHRD. (2024). Pinoy researchers advance bone repair with AI and 3D Printing. Philippine Council for Health Research and Development - DOST Article. https://www.stii.dost.gov.ph/1817-pinoy-researchers-advance-bone-repair-with-ai-and-3d-printing",
            "Full-Colorism Television | Writing program. (n.d.). © 2024 Boston University. https://www.bu.edu/writingprogram/journal/past-issues/issue-10/delossantos/#:~:text=She%20recognized%20that%20colorism%20was,the%20sun%20to%20feel%20beautiful.",
            "Bhidayasiri, R. (2024). The grand challenge at the frontiers of neurotechnology and its emerging clinical applications. Frontiers in Neurology, 15. https://doi.org/10.3389/fneur.2024.1314477",
            "Li, W., Arienzo, D., & Feusner, J. D. (2013). Body Dysmorphic Disorder: Neurobiological Features and an Updated Model. Zeitschrift Fur Klinische Psychologie Und Psychotherapie (Gottingen, Germany), 42(3), 184-191. https://doi.org/10.1026/1616-3443/a000213",
            "Regencia, Z. J. G., Gouin, J., Ladia, M. a. J., Montoya, J. C., & Baja, E. S. (2023). Effect of body image perception and skin-lightening practices on mental health of Filipino emerging adults: a mixed-methods approach protocol. BMJ Open, 13(5), e068561. https://doi.org/10.1136/bmjopen-2022-068561"
          ],
      sections: [
        {
          intro: "Key Events/Highlights",
          subintro: "From the vibrant energy of festivals like Sinulog to groundbreaking achievements in music, film, and sports, these events capture the spirit of the Philippines. Each one tells a story of celebration, triumph, and the unique way Filipinos come together to honor their heritage and showcase their talents to the world.",
        },
        {
          title: "2000-2010",
          subsections: [
          {
              title: "Social",
              subtitle: "Friendster",
              description:
                "Friendster, founded in 2002 by Jonathan Abrams, was among the pioneering social networking platforms, quickly amassing over 3 million users within months of its 2003 launch. Despite early success, it declined due to technical issues and competition from emerging platforms like MySpace and Facebook. In 2003, Friendster declined a $30 million acquisition offer from Google, a decision later viewed as a significant misstep. By 2008, the platform had over 115 million registered users, primarily in Asia. In 2009, it was acquired by Malaysia-based MOL Global for $26.4 million. Subsequently, in 2010, Facebook purchased Friendster's patents for $40 million.",
              images: [
              require("@/assets/section 1/63e303445030a75e83d8d0fe_friendster-min.webp"),

              ],
            },
            {
              title: "Economic",
              subtitle: "BPO growth and PH becomes BPO capital in 2010",
              description: "Between 2000 and 2010, the Philippines experienced significant growth in its Business Process Outsourcing (BPO) industry, transforming into a global leader in the sector. In 2000, the BPO industry contributed a modest 0.075% to the country's Gross Domestic Product (GDP). By 2005, this figure had risen to 2.4%, with the Philippines capturing over 3% of the global BPO market. The industry's expansion was driven by factors such as a highly skilled, English-proficient workforce and competitive labor costs. In 2010, the Philippines was declared the world's BPO capital, employing approximately 525,000 individuals and generating $8.9 billion in revenue. This rapid growth was further supported by government initiatives, including the establishment of the Philippine Economic Zone Authority (PEZA), which offered tax incentives and streamlined processes to attract foreign investors. The BPO sector's expansion significantly contributed to the country's economic development during this period.",
              images: [
              require("@/assets/gallery 1/bpo.jpg"),
              ],
            },
            {
              title: "Political",
              subtitle: "2000s violence by extremists",
              description: "Between 2000 and 2010, the Philippines faced significant extremist violence, primarily from groups like Abu Sayyaf and the New People's Army (NPA). In 2000, Abu Sayyaf conducted high-profile kidnappings, including the abduction of 21 individuals from Malaysia's Sipadan Island, leading to a Philippine court sentencing 17 militants to life imprisonment in 2024. In 2001, the group seized hostages from the Dos Palmas resort in Palawan, resulting in the deaths of American missionary Martin Burnham and Filipino nurse Ediborah Yap during a rescue attempt in 2002. The NPA, designated a Foreign Terrorist Organization by the U.S. in 2002, continued its insurgency, with activities peaking in 2007, making it the largest group behind terrorist attacks in the country. These events underscored the persistent threat of extremist violence in the Philippines during the decade.",
              images: [
              require("@/assets/gallery 1/extrem.webp"),
              ],
            },
            {
              title: "Cultural",
              subtitle: "Signing of the Philippine Cultural Heritage Act of 2009",
              description: "In March 2010, the Philippines enacted Republic Act No. 10066, known as the National Cultural Heritage Act of 2009.  This legislation established the Philippine Registry of Cultural Property (PRECUP) to catalog and protect the nation's cultural assets. It also mandated the preservation of historic structures over 50 years old and strengthened the National Commission for Culture and the Arts (NCCA) along with its affiliated agencies. The Act was a response to incidents like the 2000 demolition of the Manila Jai Alai Building, aiming to prevent similar losses of cultural heritage.",
              images: [
              require("@/assets/gallery 1/heritage.webp"),
              ],
            },
            {
              title: "Environmental ",
              subtitle: "Tropical Storm Ondoy 2009",
              description: "On September 26, 2009, Tropical Storm Ondoy (internationally known as Ketsana) struck the Philippines, bringing an unprecedented 455 millimeters of rainfall within 24 hours, the highest recorded in 42 years. This deluge led to severe flooding across Metro Manila and surrounding provinces, with waters reaching up to 20 feet in some areas. The disaster affected over 9.3 million people, resulted in 956 fatalities, and caused extensive damage to infrastructure and agriculture. In response, the government declared a state of calamity in Metro Manila and 25 provinces, mobilizing resources for rescue and relief operations. The event highlighted the need for improved disaster preparedness and climate resilience in the Philippines.",
              images: [
              require("@/assets/gallery 1/ondoy.jpeg"),
              ],
            },
          ],
          
        },
        {
          title: "Present Time",
          subsections: [
          {
              title: "Social",
              subtitle: "Twitter becomes X after Elon Musk acquires it for $44 billion",
              description:
                "In October 2022, Elon Musk acquired Twitter for $44 billion, initiating significant transformations within the platform. In July 2023, Musk rebranded Twitter as 'X' replacing its iconic bird logo with a stylized 'X' and redirecting the domain to x.com. This rebranding was part of Musk's vision to develop X into an 'everything app' akin to China's WeChat, integrating various services beyond social networking. The transition involved merging Twitter, Inc. into X Corp., effectively dissolving the original company structure. These changes have sparked discussions about the platform's future direction and its role in the social media landscape.",
              images: [
              require("@/assets/gallery 1/elon.webp"),
              ],
            },
            {
              title: "Economic",
              subtitle: "Philippines becomes worlds largest rice importer",
              description: "In 2023, the Philippines became the world's largest rice importer, surpassing China with 3.8 million metric tons (MMT) of imports, projected to reach 4.1 MMT in 2024. (philstar.com) Despite being the seventh-largest rice producer globally, domestic production struggles to meet rising demand due to population growth and consumption. (business.inquirer.net) Vietnam remains the top supplier, emphasizing the Philippines' dependence on imported rice to sustain its food security.",
              images: [
              require("@/assets/gallery 1/rice.jpg"),
              ],
            },
            {
              title: "Political",
              subtitle: "Philippines 'war on drugs' killings",
              description: "Between 2016 and 2022, the Philippines' 'war on drugs,'' initiated by President Rodrigo Duterte, resulted in over 6,000 reported deaths during police anti-drug operations, with human rights groups estimating the toll to be significantly higher. This campaign faced global criticism for alleged extrajudicial killings and lack of due process, sparking investigations by the International Criminal Court (ICC). Despite its controversies, the government defended the campaign as necessary for combating crime and illegal drugs, claiming it significantly reduced drug-related activities in the country.",
              images: [
              require("@/assets/gallery 1/drugwar.webp"),
              ],
            },
            {
              title: "Cultural",
              subtitle: "Celebration of Filipino Youtube Fanfest (YTFF)",
              description: "The YouTube FanFest (YTFF) in the Philippines has become a significant celebration of the country's dynamic content creators. First held in Manila in 2015, the event brought together local and international YouTube stars for performances and fan interactions. It grew annually, featuring creators like Ranz Kyle, Niana Guerrero, and Mikey Bustos. In 2021, the event adapted to a virtual format due to the pandemic, showcasing Filipino talents such as SB19 and The Juans, underscoring the continued vibrancy of the Filipino YouTube community.",
              images: [
              require("@/assets/gallery 1/fanfest.jpg"),
              ],
            },
            {
              title: "Environmental",
              subtitle: "Tropical Storm Kristine 2024",
              description: "In October 2024, Severe Tropical Storm Kristine (Trami) struck Luzon, Philippines, causing widespread flooding, landslides, and affecting over 6 million people. The storm claimed at least 116 lives, left many missing, and resulted in ₱3.76 billion in agricultural damages. States of calamity were declared in hard-hit areas, highlighting the ongoing need for stronger disaster preparedness in the country.",
              images: [
              require("@/assets/gallery 1/kristine.webp"),
              ],
            },
          ],
          
        },
        {
          title: "2030",
          subsections: [
          {
              title: "Social",
              subtitle: "A centralized hub for social media, moderated by AI, access to these platforms improve.",
              description:
                "In the future, a centralized social media hub emerges, integrating major platforms for seamless access. AI moderation ensures safer, regulated spaces by detecting harmful content in real time. Improved connectivity broadens access, making social media more inclusive and efficient for users worldwide.",
              images: [
              require("@/assets/gallery 1/centralizedhub.png"),
              ],
            },
            {
              title: "Economic",
              subtitle: "The need for importation of goods would be reduced after improvement of manufacturing capability of the Philippines.",
              description: "In the future, the Philippines' improved manufacturing capabilities reduce the need for importing goods. Enhanced local production supports domestic demand, strengthens the economy, and fosters self-sufficiency, decreasing reliance on foreign markets.",
              images: [
              require("@/assets/gallery 1/needforimportation.webp"),
              ],
            },
            {
              title: "Political",
              subtitle: "Shifts in Philippine politics beyond 2030 focus on reform, digital governance, and inclusive leadership",
              description: "After 2030, Philippine politics is expected to focus on federalism, digital governance, climate policies, and evolving regional autonomy in Bangsamoro. Leadership shifts toward younger, reform-driven figures will reflect changing voter demographics and a push for transparency and inclusive governance.",
              images: [
              require("@/assets/gallery 1/phpolitics.webp"),
              ],
            },
            {
              title: "Cultural",
              subtitle: "Filipino Culture will be mostly be curated and presented through a digital medium",
              description: "Filipino culture will be showcased and celebrated through a dynamic digital medium, blending tradition with innovation. This initiative will curate and present key aspects of Filipino heritage—arts, music, language, history, and values—through engaging, interactive, and visually compelling formats. By leveraging technology, it aims to preserve and promote the richness of Filipino identity to both local and global audiences, ensuring accessibility and inclusivity for future generations.",
              images: [
              require("@/assets/gallery 1/digitalphculture.jpg"),
              ],
            },
            {
              title: "Environmental ",
              subtitle: "Multiple typhoons hit the Philippines in succession, floods will be more severe. Adaptability of Filipinos on these calamities remains the reelevant subject.",
              description: "With multiple typhoons hitting the Philippines in succession and escalating flood severity, the resilience and adaptability of Filipinos in the face of these recurring calamities remain a critical focus. This highlights the urgent need for disaster preparedness, sustainable infrastructure, and community-driven solutions, while underscoring the enduring spirit and resourcefulness of the Filipino people.",
              images: [
              require("@/assets/gallery 1/Adaptabilityfilipinos.jpg"),
              ],
            },
          ],
          
        },
        {
          intro: "Aspect Focus: Affect Senses & Feelings",
          subintro: "From the joyful chaos of colorful festivals to the bittersweet melodies of hugot songs, every moment is designed to move the heart and awaken the senses. Imagine the comfort of traditional dishes, the warmth of a Filipino smile, or the raw emotion in a teleserye scene. Here, we explore how sights, sounds, tastes, and feelings come together to tell stories, evoke memories, and create connections that resonate deeply with the Filipino soul.",
        },
        {
          title: "2000-2010",
          subsections: [
          {
              title: "The Wowowee Stampede",
              subtitle: "The Wowowee Stampede",
              description:
                "The PhilSports Stadium Stampede (also referred to as the ULTRA stampede or the Wowowee stampede) was a crowd crush that occurred at the PhilSports Stadium (also known as the ULTRA) in Pasig, Metro Manila in the Philippines on February 4, 2006. It killed 73 people and injured about 400. About 30,000 people had gathered outside the stadium waiting to participate in the first anniversary episode of the former television variety show Wowowee.",
              images: [
              require("@/assets/gallery 1/1_16a082288a7.1665217_806339932_16a082288a7_large.jpg"),
              ],
            },
            {
              title: "Bagyong Milenyo",
              subtitle: "Bagyong Milenyo",
              description: "Bagyong Milenyo, or Typhoon Xangsane, was a devastating tropical cyclone that struck the Philippines in   September 2006. It caused widespread destruction in Luzon, resulting in severe flooding, significant infrastructure damage, and loss of life, highlighting disaster preparedness challenges. Bagyong Milenyo (Typhoon Xangsane) struck the Philippines from September 25-29, 2006, causing extensive damage and 213 fatalities. It affected over 4 million people, particularly in Metro Manila, with losses totaling P6.6 billion. The typhoon highlighted safety issues with billboards, leading to their removal after fatalities caused by falling structures",
              images: [
              require("@/assets/gallery 1/bgm1.jpg"),
              ],
            },
            {
              title: "Philippine Airlines Flight 812",
              subtitle: "Philippine Airlines Flight 812",
              description: "On May 25, 2000, Philippine Airlines Flight 812 was hijacked before landing in Manila. Armed with a gun and a grenade, the hijacker demanded valuables and attempted to escape via a homemade parachute. He died three days later when the parachute failed to deploy. Reginald Chua hijacked Philippine Airlines Flight 812, citing family abandonment as his motivation. Armed with a pistol and grenade, he demanded money before attempting to escape via parachute. His behavior during the incident raised concerns about his mental health, and his body was later found in Quezon.",
              images: [
              require("@/assets/gallery 1/pal1.jpg"),
              ],
            },
            {
              title: "Fiestas celebrated Filipino traditions through vibrant community events",
              subtitle: "Fiestas celebrated Filipino traditions through vibrant community events",
              description: "From 2000 to 2010, Filipino fiestas were vibrant celebrations that highlighted traditional culture and created profound sensory and emotional experiences. These events, deeply rooted in local traditions, combined colorful parades, intricate costumes, festive music, and dynamic performances that captivated participants and spectators. The feasts and communal gatherings brought people together to share food, laughter, and stories, strengthening bonds and fostering a deep sense of community. Beyond the visual and auditory spectacle, these festivals evoked feelings of joy, pride, nostalgia, and unity, serving as a living expression of Filipino heritage and identity.",
              images: [
              require("@/assets/gallery 1/Fiestas.webp"),
              ],
            },
            {
              title: "EDSA II",
              subtitle: "EDSA 2 inspired unity and emotional solidarity through peaceful protests.",
              description: "In 2001, EDSA 2 became a pivotal moment in Philippine history, where peaceful protests against government corruption stirred powerful emotions and a collective sense of purpose among Filipinos. Thousands gathered at the Epifanio de los Santos Avenue (EDSA), expressing outrage, hope, and solidarity through chants, songs, and shared experiences. This nonviolent movement not only demonstrated the power of unity and civic action but also left a lasting impact on the nation's collective memory, evoking pride and determination in the fight for justice and democracy.",
              images: [
              require("@/assets/gallery 1/edsa2.webp"),
              ],
            },
          ],
          
        },
        {
          title: "Present Time",
          subsections: [
          {
              title: "Impact of social media on well-being and mental health to present generations.",
              subtitle: "Impact of social media on emotional well-being and mental health of these generations.",
              description:
                "Social media has become a powerful force in shaping emotional well-being and mental health in today’s world. The constant exposure to curated content, instant feedback, and online interactions influences how people perceive themselves and others, often triggering emotions such as joy, anxiety, or inadequacy. This topic explores how social media affects the way individuals process their feelings, respond to sensory stimuli, and navigate the challenges of emotional health in an always-connected digital environment.",
              images: [
              require("@/assets/gallery 1/impactsocmed.webp"),
              ],
            },
            {
              title: "Immersive experiences in virtual reality entertainment.",
              subtitle: "Immersive experiences in virtual reality entertainment",
              description: "Virtual reality (VR) technology in popular culture is redefining how people engage with stories and experiences, offering deeply immersive environments that evoke intense emotional reactions. This topic examines how VR entertainment affects senses and feelings, exploring its ability to elicit empathy, fear, excitement, or awe through realistic simulations and interactive storytelling, shaping emotional responses in entirely new ways.",
              images: [
              require("@/assets/gallery 1/vrentertainment.webp"),
              ],
            },
            {
              title: "Influence of OPM (Original Pilipino Music) on national pride and emotional connection",
              subtitle: "Influence of OPM (Original Pilipino Music) on national pride and emotional connection",
              description: "Original Pilipino Music (OPM) has a powerful emotional impact on Filipinos, fostering feelings of nostalgia, unity, and national pride. This topic examines how popular OPM songs and artists resonate with audiences by reflecting personal and collective experiences, creating deep emotional bonds that celebrate Filipino identity and culture in the present time.",
              images: [
              require("@/assets/gallery 1/opm.png"),
              ],
            },
            {
              title: "High inflation in the Philippines",
              subtitle: "High inflation in the Philippines",
              description: "The rising cost of goods and services in the Philippines impacts how Filipinos experience their daily lives, from the sensory adjustments of cutting back on food choices to the emotional stress of financial strain. This topic examines how inflation shapes feelings of anxiety, resilience, and adaptation in the present time.",
              images: [
              require("@/assets/gallery 1/inflation.png"),
              ],
            },
            {
              title: "Decades long recurring traffic problems",
              subtitle: "Decades long recurring traffic problems",
              description: "The worsening traffic congestion in urban areas like Metro Manila directly impacts Filipinos' daily lives by inducing sensory fatigue from noise, pollution, and long commutes, while also triggering emotions such as frustration, stress, and impatience. This topic examines how these sensory and emotional challenges affect well-being in the present time.",
              images: [
              require("@/assets/gallery 1/traffic.jpg"),
              ],
            },
          ],
        },
        {
          title: "2030",
          subsections: [
          {
              title: "Climate change",
              subtitle: "Climate change",
              description:
                "The escalating effects of climate change, such as rising temperatures, extreme weather events, and environmental degradation, are likely to alter sensory and emotional experiences for future generations. This topic explores how these changes could impact daily life, from coping with physical discomfort to navigating emotional resilience in a transforming environment.",
              images: [
              require("@/assets/gallery 1/climatechange.jpg"),
              ],
            },
            {
              title: "Indigenous practices",
              subtitle: "Indigenous practices",
              description: "The preservation and adaptation of indigenous traditions in the Philippines, such as weaving, rituals, and storytelling, could impact how future generations experience their cultural identity. This topic explores how evolving practices might engage senses and feelings, blending heritage with modern influences while maintaining their cultural significance.",
              images: [
              require("@/assets/gallery 1/phindigenous.jpg"),
              ],
            },
            {
              title: "Philippines' Basketball",
              subtitle: "Philippines' Basketball",
              description: "Basketball, a deeply rooted sport in Filipino culture, is poised to evolve with the growth of international leagues, advanced training programs, and rising homegrown talents. This topic examines how these developments might impact sensory experiences, such as the excitement of live games, and evoke feelings of national pride and unity in the future.",
              images: [
              require("@/assets/gallery 1/philippinebasketball.webp"),
              ],
            },
            {
              title: "Online gambling",
              subtitle: "Online gambling",
              description: "The rise of online gambling platforms in the Philippines, driven by advancements in technology, is expected to create more immersive and engaging experiences for users. This topic examines how virtual casinos and interactive betting may affect sensory stimulation, such as vivid graphics and real-time gameplay, and evoke emotions like excitement, stress, or addiction in the coming years.",
              images: [
              require("@/assets/gallery 1/onlinegamblinng.jpg"),
              ],
            },
            {
              title: "Acceptance of LGBTQ+ norms",
              subtitle: "Acceptance of LGBTQ+ norms",
              description: "Tncreasing visibility and acceptance of LGBTQ+ individuals in the Philippines are reshaping societal interactions and personal relationships. This topic examines how this shift affects emotional experiences, such as empowerment or stigma, and sensory expressions in events like Pride marches, media representation, and inclusive spaces.",
              images: [
              require("@/assets/gallery 6/lgbtq.webp"),
              ],
            },
          ],
          
        },
        {
          intro: "Aspect Focus: Body and Self Image",
          subintro: "From traditional beauty standards influenced by history and media to the rise of body positivity and self-love movements, this journey explores how perceptions are shifting. Imagine the contrasts—skin-whitening ads alongside campaigns celebrating natural skin tones, or fitness goals shaped by both local trends and global influences. Here, every story reflects a culture in transition, balancing deep-rooted ideals with modern conversations about confidence, identity, and self-expression.",
        },
        {
          title: "2000-2010",
          subsections: [
          {
              title: "Miss International 2005 Victory",
              subtitle: "Miss International 2005 Victory",
              description:
              "In 2005, Precious Lara Quigaman's Miss International win celebrated diverse Filipino beauty and sparked national pride. This victory shifted the focus from traditional beauty standards to a more inclusive view, highlighting intelligence and cultural identity, ultimately reshaping self-image in Philippine popular culture during the decade. Precious Lara's Miss International win in 2005 influenced Philippine popular culture by promoting a broader definition of beauty. It encouraged self-acceptance and highlighted the importance of intelligence and cultural identity, leading to a more inclusive perspective on body image and self-worth during the 2000s.",
              images: [
                require("@/assets/gallery 2/2005-miss-international-winner-philippines-precious-lara-550nw-7828522b.jpg"),
              ],
            },
            {
              title: "Marian Rivera crowned as FHM Philippines' Sexiest Woman for 2008",
              subtitle: "Marian Rivera crowned as FHM Philippines' Sexiest Woman for 2008",
              description: "Marian Rivera's rise to fame through her role in the hit show Marimar led to her crowning as FHM Philippines' Sexiest Woman in 2008. This victory not only celebrated her beauty but also brought the FHM awards into Philippine households, elevating the magazine's profile and influencing popular culture. Rivera's win showcased a blend of talent and attractiveness, encouraging greater acceptance of diverse beauty standards in the process. Marian Rivera's FHM win in 2008 influenced Philippine popular culture by reinforcing beauty ideals that emphasized physical appearance. While she inspired body positivity, it also risked promoting unrealistic standards among young fans, potentially impacting their self-image and leading to pressure to conform to these ideals.",
              images: [
                require("@/assets/gallery 2/mar1.jpg"),
              ],
            },
            
            {
              title: "Emo Culture",
              subtitle: "Emo Culture",
              description: "Emo culture in the 2000s reshaped Philippine popular culture by promoting individuality and emotional expression. It influenced body image through distinctive fashion choices and encouraged discussions about mental health, allowing youth to embrace vulnerability and authenticity, ultimately transforming self-image and perceptions of beauty during the decade. Emo culture in the 2000s empowered Filipino youth by promoting individuality and personal expression. It encouraged them to embrace their unique identities and emotions, challenging societal norms and fostering a sense of belonging within a community that valued authenticity and diverse self-representation.",
              images: [
                require("@/assets/gallery 2/emo1.jpg"),
              ],
            },
            {
              title: "The start of fandoms and cosplays",
              subtitle: "The start of fandoms and cosplays",
              description: "The start of fandoms and cosplay in the Philippines from 2000 to 2010 brought significant changes to how Filipinos viewed body and self-image. As anime, gaming, and pop culture grew in popularity, cosplay became a platform for fans to embody their favorite characters, often highlighting the tension between creativity and the pressure to match specific body types. Many cosplayers faced challenges in meeting beauty standards tied to Western or East Asian influences, which shaped perceptions of self-worth and acceptance. Despite these pressures, the cosplay community became a space for Filipinos to express themselves, celebrate diversity, and redefine self-image through shared passion and creativity.",
              images: [
                require("@/assets/gallery 2/cosplay.jpg"),
              ],
            },
            {
              title: "Korean Pop Culture impact on Filipinos",
              subtitle: "Korean Pop Culture impact on Filipinos",
              description: "Korean dramas and K-pop took the Philippines by storm during the 2000s, introducing a new set of beauty ideals rooted in East Asian aesthetics. Fair, glass-like skin, slim and petite physiques, and soft, delicate features became highly admired among Filipinos. This influence spurred a surge in demand for Korean beauty products, including whitening creams and skincare routines that promised youthful, glowing skin. Many Filipinos began styling their makeup and fashion to emulate K-pop idols, further cementing these beauty ideals. However, the lack of representation of diverse body types in Korean media created unrealistic expectations, leading to dissatisfaction with one's natural appearance.",
              images: [
                require("@/assets/gallery 2/kpop.jpg"),
              ],
            },
          ],
        },
        {
          title: "Present Time",
          subsections: [
          {
              title: "Rise of TikTok and Instagram",
              subtitle: "Rise of TikTok and Instagram",
              description:
              "TikTok and Instagram heavily influence self-image through trends like “glow-ups” and body challenges. Filters and editing tools allow users to create idealized versions of themselves, which often set unrealistic beauty standards. Viral influencers, both local and international, showcase fitness routines, skincare, and cosmetic surgeries, promoting specific body types as aspirational. This constant exposure impacts how Filipinos perceive their own bodies, especially among Gen Z and Millennials. The platforms also foster body positivity movements, creating spaces for inclusivity and diverse representations of beauty.",
              images: [
                require("@/assets/gallery 2/tiktok.jpg"),
              ],
            },
            {
              title: "Body Positivity and Inclusivity in Filipino Media",
              subtitle: "Body Positivity and Inclusivity in Filipino Media",
              description: "Filipino advertisements and TV shows are beginning to highlight diverse body types, breaking away from traditional beauty standards. Brands like Dove and Bench have introduced campaigns promoting self-love, acceptance, and body positivity. This shift is empowering Filipinos to embrace their natural shapes and skin tones. However, societal pressure for lighter skin and thinner bodies persists, showing that progress remains a work in progress. The movement has sparked conversations around inclusivity and representation in mainstream media.",
              images: [
                require("@/assets/gallery 2/bodypositivity.jpg"),
              ],
            },
            
            {
              title: "Skin Whitening Practices",
              subtitle: "Skin Whitening Practices",
              description: "Despite increasing body positivity, skin-whitening products remain highly popular in the Philippines, reflecting ongoing societal preferences for lighter skin. Brands market these products as essential for confidence and beauty, reinforcing colonial beauty standards. The rise of online influencers has further normalized these practices, despite growing criticism from advocacy groups promoting skin acceptance. Filipinos are now caught between traditional ideals and modern calls for embracing natural beauty. The conversation around skin tone and identity continues to evolve, especially among the younger generation.",
              images: [
                require("@/assets/gallery 2/skinwhite.jpg"),
              ],
            },
            {
              title: "Cosmetic enhancements and the evolving beauty standards",
              subtitle: "Cosmetic enhancements and the evolving beauty standards",
              description: "Cosmetic surgeries and non-invasive treatments, such as lip fillers, nose lifts, and body contouring, have become increasingly accessible and popular in the Philippines. Social media and celebrity endorsements normalize these enhancements, with many Filipinos viewing them as a way to boost self-confidence. Clinics now cater to a younger audience, including teens, influenced by K-beauty trends and Western aesthetics. This growing acceptance of cosmetic procedures reflects a shift in Filipino attitudes toward beauty and self-image. However, it raises questions about the pressure to conform to idealized standards.",
              images: [
                require("@/assets/gallery 2/cosmeticenhancements.webp"),
              ],
            },
            {
              title: "K-Beauty and J-Beauty Trends",
              subtitle: "K-Beauty and J-Beauty Trends",
              description: "Korean and Japanese beauty trends continue to dominate the Filipino market, promoting glass skin, petite figures, and youthful appearances. Local influencers often share beauty routines and endorse products that align with these trends, further embedding them into Filipino culture. This influence pushes many Filipinos to prioritize skincare and adhere to slim body standards associated with these aesthetics. However, the popularity of these trends has also sparked discussions about the lack of representation of diverse body types and skin tones.",
              images: [
                require("@/assets/gallery 2/kbeauty.jpg"),
              ],
            },
          ],
        },
        {
          title: "2030",
          subsections: [
          {
              title: "Rise of virtual reality ",
              subtitle: "Rise of virtual reality ",
              description:
              "With the rise of virtual reality and metaverse platforms, Filipinos may increasingly design digital avatars to represent themselves, potentially changing how they perceive their physical bodies. These platforms could either reduce body-image pressures by offering limitless customization or exacerbate insecurities by promoting unrealistic digital standards. How Filipinos navigate this duality will define the future of self-expression and body image.",
              images: [
                require("@/assets/gallery 2/riseofvr.png"),
              ],
            },
            {
              title: "Advancements in cosmetic technology",
              subtitle: "Advancements in cosmetic technology",
              description: "The future of cosmetic enhancements, such as 3D-printed implants, gene-editing techniques, and non-invasive body modifications, could revolutionize beauty practices in the Philippines. These advancements might make it easier for Filipinos to achieve desired looks but could also lead to heightened pressures to undergo such procedures to fit societal standards. Ethical and cultural implications will play a major role in shaping attitudes.",
              images: [
                require("@/assets/gallery 2/cosmetictech.jpg"),
              ],
            },
            
            {
              title: "Skin tone representation",
              subtitle: "Skin tone representation",
              description: "As conversations about colorism evolve, future beauty trends in the Philippines may embrace darker skin tones, reflecting a growing appreciation for indigenous and regional features. Global beauty brands might adapt by creating products celebrating diversity, but traditional skin-whitening practices could persist, sparking ongoing cultural debates about identity and beauty.",
              images: [
                require("@/assets/gallery 2/skintone.jpg"),
              ],
            },
            {
              title: "Neurotechnology and its influence on body perception",
              subtitle: "Neurotechnology and its influence on body perception",
              description: "Advances in neurotechnology could allow Filipinos to alter how they perceive their bodies by rewiring brain responses related to self-image. This technology could reduce insecurities and promote body neutrality but might also create dependence on artificial interventions for self-acceptance. Ethical questions surrounding these technologies will shape their adoption in Filipino culture.",
              images: [
                require("@/assets/gallery 2/neurotech.jpeg"),
              ],
            },
            {
              title: "Role of education in shaping body image for the next generation",
              subtitle: "Role of education in shaping body image for the next generation",
              description: "Schools in the Philippines may integrate body positivity and mental health education into their curricula to address self-image issues early on. Programs could include discussions about social media influence, beauty standards, and self-acceptance. This proactive approach could help the next generation develop healthier attitudes toward their bodies in an increasingly digital and appearance-focused world.",
              images: [
                require("@/assets/gallery 2/bodyimage.webp"),
              ],
            },
          ],
        },
        {
          intro: "Aspect Focus: Performance",
          subintro: "Celebrate the art of performance—where every dance, every song, every act tells a story of passion and pride. Picture the vibrant moves of sinulog dancers, the powerful emotions in teleseryes, or the energy of live concerts and street festivals. Even in the digital world, performances thrive, from viral skits to online concerts. Each one is a glimpse into the soul of the Philippines—a culture that loves to express, connect, and shine.",
        },
        {
          title: "2000-2010",
          subsections: [
            {
              title: "Charice Pempengco on Oprah",
              subtitle: "Charice Pempengco on Oprah",
              description:
                "Jake Cyrus, formerly known as Charice Pempengco, captivated audiences with her 2008 appearance on The Oprah Winfrey Show, showcasing Filipino talent on a global stage. Her powerful performances inspired national pride and encouraged aspiring artists, marking a significant moment in Philippine popular culture during the 2000s. Jake Cyrus's 2008 appearance on Oprah instilled a deep sense of pride among Filipino youth, as they saw one of their own achieving global recognition. This milestone inspired them to embrace their cultural identity and aspire to showcase their talents on an international stage.",
              images: [
              require("@/assets/gallery 5/char1.jpg"),
              ],
            },
            {
              title: "Local Films like Magnifico, One More Chance, & Tanging Yaman",
              subtitle: "Local Films like Magnifico, One More Chance, & Tanging Yaman",
              description: "The success of local films like Magnifico, One More Chance, and Tanging Yaman in the 2000s showcased powerful performances and emphasized family values. These movies resonated with audiences, fostering cultural pride and identity while elevating Philippine cinema as a significant force in the entertainment landscape during the decade. The success of local films in the 2000s instilled a sense of accomplishment as these award-winning movies garnered international recognition. This achievement fostered pride among Filipinos, motivating them to celebrate their cultural contributions and engage more deeply with their heritage.",
              images: [
              require("@/assets/gallery 5/fil1.webp"),
              ],
            },
            {
              title: "Sexbomb Girls - The Spageti Song",
              subtitle: "Sexbomb Girls - The Spageti Song",
              description: "The Sexbomb Girls rose to fame through their appearances on Eat Bulaga in the 2000s, captivating audiences with their hit 'The Spaghetti Song'. Their catchy music, playful choreography, and humor celebrated fun and lightheartedness, significantly impacting Philippine popular culture and evolving standards of femininity.",
              images: [
              require("@/assets/gallery 5/spag1.jpg"),
              ],
            },
            {
              title: "Reality Talent Shows",
              subtitle: "Reality Talent Shows",
              description: "Shows like “Starstruck,” “Pinoy Big Brother,” and “Philippine Idol” revolutionized the way Filipino talent was discovered and celebrated. These programs gave ordinary individuals a platform to showcase their singing, acting, or dancing skills, with the promise of instant fame. The competitive nature of these shows pushed contestants to deliver standout performances, raising the bar for live entertainment. They also reflected shifting audience preferences, emphasizing relatability and authenticity. This boom shaped a generation of Filipino performers who became household names and industry icons.",
              images: [
              require("@/assets/gallery 5/realityshow.png"),
              ],
            },
            {
              title: "K-Pop dance covers",
              subtitle: "K-Pop dance covers",
              description: "Early 2000s marked the emergence of K-pop dance cover groups in the Philippines, inspired by groups like Super Junior and Girls' Generation. These amateur performers replicated intricate choreographies in malls, school events, and competitions. The trend fostered a new kind of performance culture where precision, synchronization, and stage presence became paramount. It also introduced Filipinos to new performance techniques influenced by Korean training systems. These early adopters of K-pop dance laid the groundwork for the current boom in Filipino dance troupes.",
              images: [
              require("@/assets/gallery 5/kpopdancecover.jpg"),
              ],
            },
          ],
        },
        {
          title: "Present Time",
          subsections: [
            {
              title: "TikTok",
              subtitle: "TikTok",
              description:
                "TikTok has become the dominant platform for performance, enabling Filipinos to showcase their talents in singing, dancing, acting, and even comedy. With short, engaging videos, performers can quickly reach global audiences, bypassing traditional media. The app's algorithm rewards creativity and consistency, making it easier for undiscovered talent to gain popularity. Dance trends, lip-sync battles, and original skits have become key avenues for expression, redefining what it means to perform in the digital age. This shift has also blurred the line between amateur and professional performers, allowing everyday Filipinos to become influential content creators.",
              images: [
              require("@/assets/gallery 5/tiktokinph.jpg"),
              ],
            },
            {
              title: "Filipino drag performances",
              subtitle: "Filipino drag performances",
              description: "Drag culture in the Philippines has gained mainstream recognition through shows like 'Drag Den' and 'Drag Race Philippines.' Drag queens now blend lip-syncing, comedy, and fashion into highly theatrical performances that challenge traditional gender norms. These shows have created new opportunities for LGBTQ+ performers, fostering acceptance and visibility. Drag bars and competitions have become thriving hubs for creativity, showcasing the unique blend of humor, drama, and artistry in Filipino drag performances.",
              images: [
              require("@/assets/gallery 5/drag.webp"),
              ],
            },
            {
              title: "Social media livestreams",
              subtitle: "Social media livestreams",
              description: "Livestreaming platforms like Kumu, Facebook Live, and YouTube Live have become essential tools for Filipino performers to connect with audiences. Singers, bands, and comedians use these streams to perform in real time, often engaging directly with fans through chat. These livestreams allow performers to earn income through virtual gifts and sponsorships while maintaining intimate connections with their audiences. This interactive form of performance has changed how Filipinos consume entertainment, prioritizing accessibility and personal engagement.",
              images: [
              require("@/assets/gallery 5/livestreamkumu.jpg"),
              ],
            },
            {
              title: "Dance competitions",
              subtitle: "Dance competitions",
              description: "Dance competitions remain a vital part of Filipino youth culture, with groups like UPeepz and A-Team gaining international acclaim. These teams often combine hip-hop, contemporary, and cultural dance elements in their routines, showcasing the versatility of Filipino performers. Competitions, both local and international, push dancers to innovate and achieve technical mastery. The inclusion of digital platforms like YouTube and Instagram has allowed these performances to reach global audiences, inspiring the next generation of Filipino dancers.",
              images: [
              require("@/assets/gallery 5/dancecompetition.jpg"),
              ],
            },
            {
              title: "Festival performances",
              subtitle: "Festival performances",
              description: "Philippine festivals like Sinulog, Panagbenga, and MassKara now incorporate cutting-edge technology, including LED lighting, drones, and 3D mapping, to enhance their traditional performances. Dance and music are still at the core, but the visual spectacle has become a major draw for younger audiences. These performances continue to celebrate Filipino culture while adapting to modern tastes and technological advancements, creating a fusion of tradition and innovation.",
              images: [
              require("@/assets/gallery 5/festivalperformance.jpg"),
              ],
            },
          ],
        },
        {
          title: "2030",
          subsections: [
            {
              title: "Augmented Reality (AR) in Live Filipino Performances",
              subtitle: "Augmented Reality (AR) in Live Filipino Performances",
              description:
                "Future live performances in the Philippines will integrate AR to create immersive experiences for audiences. Concerts and theater productions could use AR to overlay digital effects onto live acts, allowing performers to interact with holographic elements in real time. This technology would elevate storytelling, giving performers a more dynamic stage to work with and audiences a fully engaging visual spectacle. AR has the potential to transform traditional performances into hybrid digital-physical experiences, attracting younger, tech-savvy audiences.",
              images: [
              require("@/assets/gallery 5/augmentedreality.jpg"),
              ],
            },
            {
              title: "AI-Generated Performers",
              subtitle: "AI-Generated Performers",
              description: "AI-generated singers, dancers, and influencers could dominate the entertainment industry, with virtual performers headlining concerts and creating content online. These digital personalities, designed to meet evolving trends, might collaborate with human performers or even replace them in certain contexts. While this innovation could lower production costs and cater to niche audiences, it raises questions about authenticity and the value of human creativity in performances. Filipino audiences will likely grapple with balancing their love for genuine talent and fascination with futuristic entertainment.",
              images: [
              require("@/assets/gallery 5/aigeneratedperformers.webp"),
              ],
            },
            {
              title: "Personalized Performances Using Virtual Reality (VR)",
              subtitle: "Personalized Performances Using Virtual Reality (VR)",
              description: "VR will redefine how performances are experienced, allowing Filipino audiences to step into fully immersive environments. Viewers could attend virtual concerts, plays, or dance shows from the comfort of their homes, feeling as though they are in the middle of the action. Performers may create interactive, personalized experiences where audiences can choose their perspectives or even interact with the performance. This shift could redefine the relationship between performers and their audiences, offering new creative opportunities.",
              images: [
              require("@/assets/gallery 5/personalizedperformancesvr.webp"),
              ],
            },
            {
              title: "Audience Biometrics",
              subtitle: "Audience Biometrics",
              description: "Performances may adapt dynamically based on real-time audience reactions measured through biometrics like heart rate, facial expressions, org applause levels. Filipino performers could use wearable tech or audience-linked sensors to adjust their delivery, choreography, or pacing during a show. This interactive feedback loop would make performances more engaging and personalized, creating a deeper connection between performers and their audiences.",
              images: [
              require("@/assets/gallery 5/audiencebiometrics.jpg"),
              ],
            },
            {
              title: "AI-Generated Music and Choreography",
              subtitle: "AI-Generated Music and Choreography",
              description: "AI tools may become integral to the creative process in Filipino music, dance, and theater. AI-generated songs and dance routines will assist performers in developing content more efficiently, tailored to audience preferences. Musicians might use AI to create custom tracks for performances, while choreographers use it to design innovative routines. While AI will enhance creativity, debates will persist about its role in replacing human ingenuity and the authenticity of AI-driven performances.",
              images: [
              require("@/assets/gallery 5/aigeneratedmusic.webp"),
              ],
            },
          ],
        },
        {
          intro: "Overall Observable Trends",
          subintro: "Explore the patterns shaping how Filipinos live, create, and connect. From the rise of K-pop and binge-worthy dramas to the growing influence of social media and streaming platforms, you'll see how global and local influences blend seamlessly. Discover how traditional values meet modern lifestyles, how OPM continues to evolve, and how gaming and digital trends are reshaping youth culture. These trends are like pieces of a puzzle, showing the ever-changing story of the Filipino spirit.",
        },
        {
          title: "2000-2010",
          subsections: [
            {
              title: "Media",
              subtitle: "Media",
              description:
                "The 2000s saw Filipino audiences increasingly exposed to global entertainment due to advancements in cable TV, DVDs, and the internet. Korean dramas, Western pop music, and Hollywood blockbusters heavily influenced Filipino tastes and performance styles. This period marked a shift toward international trends in fashion, music, and entertainment, blending global influences with Filipino culture.",
              images: [
              require("@/assets/gallery 5/dvdinph.jpg"),
              ],
            },
            {
              title: "Rise of Reality TV and Talent Competitions",
              subtitle: "Rise of Reality TV and Talent Competitions",
              description: "Reality TV became a dominant genre in Philippine media, with shows like 'Pinoy Big Brother,' 'StarStruck,' and 'Philippine Idol.' These programs created platforms for aspiring performers and emphasized audience participation through voting systems. This trend democratized talent discovery, giving ordinary Filipinos opportunities to rise to fame while fostering a national obsession with reality-based entertainment.",
              images: [
              require("@/assets/gallery 5/realitytv.jpg"),
              ],
            },
            {
              title: "Digital and Mobile Technology",
              subtitle: "Digital and Mobile Technology",
              description: "The widespread adoption of mobile phones and internet cafes during this decade revolutionized communication and entertainment. Filipinos embraced texting (SMS) culture, using it not only for social interaction but also to vote in reality shows and participate in contests. This period also saw the rise of social networking platforms like Friendster and Multiply, where Filipinos showcased their creativity and self-expression.",
              images: [
              require("@/assets/gallery 5/smsculture.webp"),
              ],
            },
            {
              title: "Original Filipino Music (OPM)",
              subtitle: "Original Filipino Music (OPM)",
              description: "2000s marked a resurgence of interest in Original Pilipino Music (OPM), with bands like Bamboo, Parokya ni Edgar, and Rivermaya dominating the airwaves. The rise of acoustic music by artists like Aiza Seguerra and Paolo Santos further diversified the OPM landscape. Live performances at bars and music festivals gained popularity, fostering a stronger connection between artists and fans.",
              images: [
              require("@/assets/gallery 5/opm2000.jpg"),
              ],
            },
            {
              title: "Cultural Festivals",
              subtitle: "Cultural Festivals",
              description: "Traditional festivals like Sinulog, MassKara, and Kadayawan began incorporating contemporary music, dance, and staging techniques to attract younger audiences. These events retained their cultural roots while modernizing their presentation to keep up with evolving tastes. The blend of tradition and innovation highlighted Filipinos' adaptability and creativity.",
              images: [
              require("@/assets/gallery 5/sinulog.jpg"),
              ],
            },
          ],
        },
        {
          title: "Present Time",
          subsections: [
            {
              title: "Representation and Diversity in Media",
              subtitle: "Representation and Diversity in Media",
              description:
                "Media and entertainment in the Philippines are beginning to embrace more diverse body types, skin tones, and gender identities. Campaigns like body positivity movements and LGBTQ+ representation in shows and films reflect a shift toward inclusivity. While traditional beauty standards still hold influence, younger audiences demand authentic representation and narratives that resonate with their experiences.",
              images: [
              require("@/assets/gallery 5/representation.png"),
              ],
            },
            {
              title: "Integration of Technology in Live Performances",
              subtitle: "Integration of Technology in Live Performances",
              description: "Filipino concerts, theater productions, and festivals are increasingly incorporating advanced technology like AR, VR, and 3D projections. Events now blend physical and digital experiences to create immersive spectacles that attract tech-savvy audiences. Virtual concerts and hybrid events, which became popular during the pandemic, continue to thrive, allowing performers to connect with audiences both locally and globall",
              images: [
              require("@/assets/gallery 5/technologyinlive.jpg"),
              ],
            },
            {
              title: "Filipino Talents",
              subtitle: "Filipino Talents",
              description: "Filipino performers are gaining more recognition on the global stage, with artists like SB19, Bella Poarch, and H.E.R. making waves internationally. Social media and streaming platforms like Spotify and YouTube have played crucial roles in showcasing Filipino creativity to global audiences. This trend has led to increased pride in local talent and a stronger push for more Filipino representation in international media.",
              images: [
              require("@/assets/gallery 5/sb19.jpg"),
              ],
            },
            {
              title: "E-Sports and Gaming",
              subtitle: "E-Sports and Gaming",
              description: "Gaming has become a dominant form of entertainment in the Philippines, with professional e-sports leagues, streaming platforms, and gaming influencers capturing large audiences. Performances in gaming, such as live-streamed gameplay or virtual tournaments, are viewed as competitive and artistic expressions. This trend has created new opportunities for performers and athletes in the gaming industry.",
              images: [
              require("@/assets/gallery 5/esports.jpg"),
              ],
            },
            {
              title: "Mental Health and Wellness",
              subtitle: "Mental Health and Wellness",
              description: "The entertainment industry is addressing mental health more openly, with themes related to anxiety, depression, and self-care appearing in TV shows, films, and online content. Performers are also using their platforms to advocate for mental health awareness, fostering discussions around emotional well-being. This shift reflects the growing importance of holistic self-expression in performance and art.",
              images: [
              require("@/assets/gallery 5/mentalhealth.jpg"),
              ],
            },
          ],
        },
        {
          title: "Impact of the Past to Present Trend",
          subsections: [
            {
              title: "Filipino Pop Culture",
              subtitle: "Filipino Pop Culture",
              description:
                "The exposure to global entertainment in the 2000s—through cable TV, DVDs, and the internet—paved the way for the widespread adoption of international trends today. Korean dramas and Western pop music, introduced in the 2000s, have evolved into mainstream preferences, with K-pop dominating Filipino music charts and global streaming platforms expanding Filipino access to diverse content. The cultural fusion of past and present is evident in how Filipinos incorporate global influences into their local artistry.",
              images: [
              require("@/assets/gallery 5/internetinph.jpg"),
              ],
            },
            {
              title: "From Reality TV to Social Media Fame",
              subtitle: "From Reality TV to Social Media Fame",
              description: "The rise of reality TV in the 2000s democratized access to fame, a concept that has evolved with social media platforms like TikTok and YouTube. Shows like Pinoy Big Brother introduced the idea of audience participation in talent discovery, which has now transitioned to likes, shares, and comments as a measure of success. Today's influencers and creators owe much to the participatory culture of the 2000s, where fans first shaped public recognition.",
              images: [
              require("@/assets/gallery 5/pbb.webp"),
              ],
            },
            {
              title: "Beauty Standards",
              subtitle: "Beauty Standards",
              description: "Skin-whitening trends of the 2000s have left a lingering impact on Filipino beauty standards, although there is a growing movement toward inclusivity and natural skin tones today. While whitening products remain popular, the rise of global campaigns promoting diversity and the body positivity movement have sparked a shift in perceptions. Past colonial ideals still shape beauty standards, but present trends reflect a growing resistance to such norms.",
              images: [
              require("@/assets/gallery 5/skinwhiteningph.jpg"),
              ],
            },
            {
              title: "SMS to Social Media",
              subtitle: "SMS to Social Media",
              description: "The texting (SMS) culture of the 2000s, used for voting in reality shows and connecting with friends, has evolved into full-scale social media activism and engagement. The participatory mindset instilled during this period now drives campaigns, crowdfunding, and fandom support for artists on platforms like Twitter and Facebook. Social media trends owe much to the interactive culture initiated during the 2000s.",
              images: [
              require("@/assets/gallery 5/textingculture.jpg"),
              ],
            },
            {
              title: "Indie Films",
              subtitle: "Indie Films",
              description: "The indie film movement, which gained momentum in the 2000s through festivals like Cinemalaya, has propelled Filipino filmmakers to global stages today. The bold storytelling and artistic experimentation introduced during this period continue to inspire modern directors, with many receiving international acclaim. Streaming platforms have further amplified the reach of Filipino indie films, solidifying their cultural impact.",
              images: [
              require("@/assets/gallery 5/indiefilms.jpg"),
              ],
            },
          ],
        },
        {
          title: "Impact to 2030",
          subsections: [
          {
              title: "Digital Education",
              subtitle: "Digital Education",
              description: "The increasing popularity of online learning platforms will make arts education more accessible by 2030. Filipino performers will benefit from virtual masterclasses, AI-driven training, and online mentorship, breaking barriers for those in rural areas. Current trends in e-learning, coupled with advancements in AI, will allow aspiring artists to refine their skills without the need for traditional institutions. This will democratize arts education but may lead to a saturation of talent competing for limited opportunities.",
              images: [
              require("@/assets/gallery 5/onlinelearning.jpg"),
              ],
            },
            {
              title: "AI-Generated Contents",
              subtitle: "AI-Generated Contents",
              description:
                "AI will play a significant role in creating performances by 2030, with AI-generated music, choreography, and even virtual performers becoming mainstream. Filipino artists will use AI tools to enhance creativity and efficiency, tailoring performances to audience preferences. Virtual performers and avatars will collaborate with human artists, blending artificial intelligence with human creativity. This will spark debates on authenticity and redefine the boundaries of performance art.",
              images: [
              require("@/assets/gallery 5/aigencollab.jpg"),
              ],
            },
            {
              title: "Representation and Inclusion in Media",
              subtitle: "Representation and Inclusion in Media",
              description: "Current advocacy for diversity and inclusion will likely transform Filipino media by 2030. Representation of different body types, skin tones, gender identities, and abilities will become standard in performances, films, and advertising. This shift will encourage more authentic storytelling and foster greater self-acceptance among audiences, shaping societal perceptions of beauty and talent.",
              images: [
              require("@/assets/gallery 5/representationbodytypes.jpg"),
              ],
            },
            {
              title: "Traditional Arts",
              subtitle: "Traditional Arts",
              description: "Efforts to preserve Filipino cultural heritage today will bear fruit by 2030, with AR and VR technologies bringing traditional dances, music, and festivals to life for younger generations. Immersive experiences will allow audiences to interact with cultural performances and historical narratives, ensuring that tradition remains relevant in a digital-first world. Filipino artists will lead this fusion of heritage and innovation, exporting cultural performances globally.",
              images: [
              require("@/assets/gallery 5/tradart.jpg"),
              ],
            },
            {
              title: "E-Sports",
              subtitle: "E-Sports",
              description: "The rapid growth of gaming culture and e-sports in the Philippines, driven by improved internet access and affordable gaming setups, will make it a dominant entertainment sector by 2030. Filipino gamers and teams will compete globally, and e-sports events will rival traditional performances in terms of audience size and engagement. Platforms like Twitch and YouTube Gaming will elevate gaming as both a sport and a performance, with opportunities for storytelling, audience interaction, and even sponsorships rivaling traditional media.",
              images: [
              require("@/assets/gallery 5/esportsph.webp"),
              ],
            },
          ],
        },
      ],
    
      
      showModal: false,
      activeRoom: {},
    };
  },
  mounted() {
    const appContainer = document.getElementById("app");
    appContainer.addEventListener("wheel", this.handleMouseWheel, {
      passive: false,
    });
  },
  beforeUnmount() {
    const appContainer = document.getElementById("app");
    appContainer.removeEventListener("wheel", this.handleMouseWheel);
  },
  methods: {
    getBackgroundStyle(index) {
      const backgrounds = [
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492121/Teambangan%20Museum/BG%20Covers/redcover_sfwfpp.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492076/Teambangan%20Museum/BG%20Covers/1_zcohw5.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492116/Teambangan%20Museum/BG%20Covers/2_euirfg.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492102/Teambangan%20Museum/BG%20Covers/3_hwuijn.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492121/Teambangan%20Museum/BG%20Covers/redcover_sfwfpp.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492790/Teambangan%20Museum/BG%20Covers/4_flcvhx.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492786/Teambangan%20Museum/BG%20Covers/5_lewnrq.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492120/Teambangan%20Museum/BG%20Covers/6_gcm8qt.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492121/Teambangan%20Museum/BG%20Covers/redcover_sfwfpp.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492791/Teambangan%20Museum/BG%20Covers/7_fvl4pd.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492796/Teambangan%20Museum/BG%20Covers/8_jadv1m.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492114/Teambangan%20Museum/BG%20Covers/10_cscizq.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492121/Teambangan%20Museum/BG%20Covers/redcover_sfwfpp.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732493116/Teambangan%20Museum/BG%20Covers/9_hdegd_ewy0pd.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492791/Teambangan%20Museum/BG%20Covers/11_xzcgnv.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492112/Teambangan%20Museum/BG%20Covers/12_hdwh5t.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492121/Teambangan%20Museum/BG%20Covers/redcover_sfwfpp.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492787/Teambangan%20Museum/BG%20Covers/15_e7skfn.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492785/Teambangan%20Museum/BG%20Covers/16_aqvgnr.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492116/Teambangan%20Museum/BG%20Covers/14_dyddvk.png'}, 
        { type: 'image', value: 'https://res.cloudinary.com/dk3aalcb0/image/upload/v1732492108/Teambangan%20Museum/BG%20Covers/13_ofecyg.png'}, 
      ];

      const bg = backgrounds[index % backgrounds.length]; // Cycle through backgrounds

      if (bg.type === 'color') {
        return { backgroundColor: bg.value }; // Return background color style
      } else if (bg.type === 'image') {
        return {
          backgroundImage: `url(${bg.value})`,
          backgroundSize: 'cover',
          backgroundRepeat: 'no-repeat',
          backgroundPosition: 'center',
        }; // Return background image style
      }

      return { backgroundColor: '#FFFFFF' }; // Default fallback
    },
    scrollToNextSectionFromHeader() {
      const target = document.getElementById("group-section"); // Ensure ID matches
      if (target) {
        target.scrollIntoView({ behavior: "smooth" }); // Smooth scrolling
      }
    },
    openVirtualRoom(sectionIndex, subsectionIndex) {
      this.activeRoom =
        this.sections[sectionIndex].subsections[subsectionIndex];
      this.showModal = true;
    },
    closeVirtualRoom() {
      this.showModal = false;
      this.activeRoom = {};
    },
    handleMouseWheel(event) {
      event.preventDefault(); // Prevent default scroll behavior
      const scrollAmount = event.deltaY > 0 ? 100 : -100; // Adjust scroll speed
      window.scrollBy({
        top: scrollAmount,
        behavior: "smooth", // Smooth scrolling
      });
    },
  },

};
</script>


<style src="./styles.css"></style>
