# aGents.md - EnbabelLATAM Agent Framework
## *Agentes Inteligentes para América Latina - "En Babel, LATAM"*

> **Pronunciation Guide**: Ask your amigo/amiga latinoamericano/a to pronounce it - they'll know the prosodic accent. Trust the unique resonance that speaks to your soul. 🎵

---

## 🌎 Vision LATAM

**EnbabelLATAM** represents the democratization of AI agent technology for Latin America, built on the solid foundation of the JVM with the cultural wisdom and community spirit that defines our región.

### Core Philosophy
- **Inclusive Technology**: AI agents should speak the languages and understand the cultural contexts of LATAM
- **Community-Driven**: Following the "minga" principle - collective work for collective benefit
- **Bridge Building**: Like the original Tower of Babel, but this time we're building bridges, not barriers

---

## 🏗️ Agent Architecture Overview

### The LATAM Stack
```
┌─────────────────────────────────────────────────────────┐
│                    aGent Layer                          │
│  (Spanish/Portuguese/Indigenous Language Support)       │
├─────────────────────────────────────────────────────────┤
│              Embabel Framework (JVM)                    │
│        (Kotlin/Java + Spring + GOAP Planning)          │
├─────────────────────────────────────────────────────────┤
│                Cultural Context Layer                   │
│     (Regional Calendars, Currencies, Time Zones)       │
├─────────────────────────────────────────────────────────┤
│                 LLM Integration                         │
│  (OpenAI, Anthropic, Ollama, Local Models)            │
└─────────────────────────────────────────────────────────┘
```

### Key Differentiators
1. **Multi-idioma Support**: Native Spanish, Portuguese, and Indigenous language processing
2. **Cultural Context Awareness**: Understanding of LATAM business practices, holidays, currencies
3. **Community Sharing**: Built-in mechanisms for sharing agents across LATAM communities
4. **Economic Accessibility**: Optimized for cost-effective deployment in emerging markets

---

## 🤖 Core Agent Types

### 1. MercadoLibre Agent (`@Agent MercadoLibreBot`)
**Purpose**: E-commerce automation for Latin America's largest marketplace

```kotlin
@Agent(description = "Automatiza operaciones en MercadoLibre para vendedores LATAM")
class MercadoLibreAgent(
    private val mercadoLibreService: MercadoLibreService,
    private val currencyConverter: LatamCurrencyService
) {
    
    @Action
    fun analizarPrecios(producto: ProductoInput): AnalisisPrecio =
        PromptRunner().createObject("""
            Analiza los precios de "${producto.nombre}" en MercadoLibre 
            considerando las diferencias regionales en LATAM.
            Incluye análisis de:
            - Precio promedio por país (México, Argentina, Brasil, Colombia, Chile)
            - Variaciones estacionales 
            - Competencia local
            - Recomendaciones de pricing estratégico
        """)
    
    @AchievesGoal(description = "Optimizar listing de producto para máxima visibilidad")
    @Action
    fun optimizarListing(
        producto: ProductoInput,
        analisisPrecios: AnalisisPrecio
    ): ListingOptimizado =
        PromptRunner().createObject("""
            Crea un listing optimizado para MercadoLibre considerando:
            - SEO keywords en español/português
            - Estructura de precios regional
            - Descripción culturalmente apropiada
            - Estrategia de envío para LATAM
        """)
}
```

### 2. Fintech Agent (`@Agent FintechLatam`)
**Purpose**: Financial operations adapted to LATAM banking and payment systems

```kotlin
@Agent(description = "Maneja operaciones financieras con contexto LATAM")
class FintechLatamAgent(
    private val bancoService: BancoLatamService,
    private val pagosService: PagosLatamService
) {
    
    @Action
    fun convertirMonedas(monto: MontoInput): ConversionLatam =
        PromptRunner().createObject("""
            Convierte ${monto.cantidad} ${monto.monedaOrigen} considerando:
            - Tasas de cambio oficiales vs blue/paralelas (especialmente ARG)
            - Comisiones bancarias típicas en ${monto.paisDestino}
            - Mejor método de transferencia (SWIFT, remesas, crypto)
            - Implicaciones fiscales locales
        """)
    
    @Action(toolGroups = [ToolGroup.BANKING])
    fun procesarPago(conversion: ConversionLatam): ResultadoPago =
        PromptRunner().createObject("""
            Procesa el pago utilizando el mejor método para ${conversion.paisDestino}:
            - PSE (Colombia), PIX (Brasil), Interbank (Perú)
            - Considera horarios bancarios locales
            - Valida documentos según normativas locales
        """)
}
```

### 3. Content Creator Agent (`@Agent CreadorContenidoLatam`)
**Purpose**: Generate culturally relevant content for LATAM audiences

```kotlin
@Agent(description = "Crea contenido culturalmente relevante para audiencias LATAM")
class CreadorContenidoLatamAgent(
    private val calendarioService: CalendarioLatamService,
    private val trendsService: TrendsLatamService
) {
    
    @Action
    fun analizarContextoCultural(tema: TemaInput): ContextoCultural =
        PromptRunner().createObject("""
            Analiza el contexto cultural de "${tema.contenido}" para ${tema.paisObjetivo}:
            - Referencias culturales apropiadas
            - Eventos/fechas importantes locales
            - Tono y estilo de comunicación preferido
            - Sensibilidades culturales a evitar
            - Jerga y modismos locales relevantes
        """)
    
    @AchievesGoal(description = "Generar contenido viral para redes sociales LATAM")
    @Action
    fun crearContenidoViral(
        contexto: ContextoCultural,
        plataforma: PlataformaInput
    ): ContenidoViral =
        PromptRunner().withTemperature(1.3).createObject("""
            Crea contenido viral para ${plataforma.nombre} dirigido a ${contexto.pais}:
            
            Contexto cultural: ${contexto.referencias}
            
            Requisitos:
            - Usar modismos locales apropiados
            - Incluir referencias culturales relevantes
            - Optimizar para engagement en ${plataforma.nombre}
            - Considerar horarios de mayor actividad en la región
            - Incluir hashtags trending locales
            
            Formato: ${plataforma.formatoPreferido}
        """)
}
```

---

## 🔧 LATAM-Specific Features

### Cultural Context Integration

#### Time Zone Management
```kotlin
data class EventoLatam(
    val descripcion: String,
    val fechaHora: ZonedDateTime,
    val pais: PaisLatam,
    val consideracionesCulturales: List
) {
    @Tool
    fun ajustarParaZonaHoraria(paisDestino: PaisLatam): EventoLatam {
        val nuevaFecha = fechaHora.withZoneSameInstant(paisDestino.zonaHoraria)
        return copy(
            fechaHora = nuevaFecha,
            consideracionesCulturales = consideracionesCulturales + 
                "Ajustado para ${paisDestino.nombre} (${paisDestino.zonaHoraria})"
        )
    }
}
```

#### Currency and Economic Context
```kotlin
data class MonedaLatam(
    val codigo: String,
    val nombre: String,
    val simbolo: String,
    val inflacionAnual: Double,
    val volatilidad: VolatilidadLevel
) {
    @Tool
    fun calcularPoderAdquisitivo(monto: Double, paisReferencia: PaisLatam): Double {
        // Implement PPP calculations for LATAM context
        return when (paisReferencia) {
            ARGENTINA -> monto * factorInflacionArg()
            VENEZUELA -> monto * factorInflacionVen()
            else -> monto * factorEstandar()
        }
    }
}
```

#### Language and Localization
```kotlin
enum class IdiomaLatam(
    val codigo: String,
    val nombre: String,
    val variantes: List
) {
    ESPAÑOL_MX("es-MX", "Español México", listOf("mexicano", "norteño")),
    ESPAÑOL_AR("es-AR", "Español Argentina", listOf("rioplatense", "porteño")),
    ESPAÑOL_CO("es-CO", "Español Colombia", listOf("bogotano", "costeño")),
    PORTUGUÊS_BR("pt-BR", "Português Brasil", listOf("paulista", "carioca", "nordestino")),
    GUARANÍ("gn", "Guaraní", listOf("paraguayo", "argentino")),
    QUECHUA("qu", "Quechua", listOf("cusqueño", "boliviano"))
}
```

---

## 🚀 Quick Start LATAM

### 1. Setup Your Environment
```bash
# Clone the LATAM fork
git clone https://github.com/SorretAI/enbabel-agent_LATAM.git
cd enbabel-agent_LATAM

# Set your API keys (support for local models encouraged)
export OPENAI_API_KEY="tu_key_aquí"
export ANTHROPIC_API_KEY="tu_key_anthropic"
export HUGGINGFACE_API_KEY="para_modelos_locales"

# LATAM-specific configurations
export LATAM_REGION="MEXICO"  # or ARGENTINA, BRASIL, COLOMBIA, etc.
export PREFERRED_LANGUAGE="es-MX"
export LOCAL_CURRENCY="MXN"
```

### 2. Run Your First LATAM Agent
```bash
./scripts/run-latam.sh

# En el shell interactivo:
execute "Ayúdame a optimizar mi negocio de tacos para MercadoLibre México"
execute "Crea contenido viral sobre el Día de los Muertos para TikTok"
execute "Convierte 1000 USD a pesos argentinos considerando el dólar blue"
```

### 3. Create Your Own LATAM Agent
```kotlin
@Agent(description = "Tu agente personalizado para LATAM")
class MiAgenteLatam(
    private val contextoLatam: ContextoLatamService
) {
    
    @Action
    fun procesarSolicitudLocal(solicitud: SolicitudInput): RespuestaLatam {
        val contexto = contextoLatam.obtenerContexto(solicitud.pais)
        
        return PromptRunner().createObject("""
            Procesa la siguiente solicitud considerando el contexto de ${solicitud.pais}:
            "${solicitud.descripcion}"
            
            Contexto local:
            - Zona horaria: ${contexto.zonaHoraria}
            - Moneda local: ${contexto.moneda}
            - Idioma preferido: ${contexto.idioma}
            - Consideraciones culturales: ${contexto.cultura}
        """)
    }
}
```

---

## 🌟 Advanced LATAM Features

### Federation Across LATAM
```kotlin
// Connect agents across borders
@Configuration
class FederacionLatamConfig {
    
    @Bean
    fun redLatamAgentes(): FederacionAgentes {
        return FederacionAgentes.builder()
            .nodoMexico("https://mexico.enbabel-latam.com")
            .nodoArgentina("https://argentina.enbabel-latam.com")
            .nodoBrasil("https://brasil.enbabel-latam.com")
            .protocolo(ProtocoloLatam.SEGURO)
            .autenticacion(AuthLatam.OAUTH_LATAM)
            .build()
    }
}
```

### Economic Intelligence
```kotlin
@Agent(description = "Inteligencia económica para decisiones LATAM")
class EconomiaLatamAgent {
    
    @Action(toolGroups = [ToolGroup.ECONOMIC_DATA])
    fun analizarIndicadoresEconomicos(pais: PaisLatam): AnalisisEconomico =
        PromptRunner().createObject("""
            Analiza los indicadores económicos actuales de ${pais.nombre}:
            - Inflación mensual y anual
            - Tipo de cambio oficial vs paralelo
            - Índice de confianza del consumidor
            - Principales riesgos políticos/económicos
            - Oportunidades de inversión
            - Recomendaciones para empresas
        """)
}
```

### Cultural Event Intelligence
```kotlin
@Agent(description = "Inteligencia de eventos culturales LATAM")
class EventosCulturalesAgent {
    
    @Action
    fun proximosEventosCulturales(region: RegionLatam): CalendarioCultural =
        PromptRunner().createObject("""
            Lista los próximos eventos culturales importantes en ${region.nombre}:
            - Festivales nacionales y regionales
            - Días feriados únicos de la región
            - Eventos deportivos (fútbol, baseball, etc.)
            - Celebraciones religiosas
            - Ferias comerciales importantes
            - Implicaciones para marketing y ventas
        """)
}
```

---

## 🎭 Community & Collaboration

### LATAM Developer Network
- **Discord**: [EnbabelLATAM Community](https://discord.gg/enbabel-latam)
- **WhatsApp Groups**: Por país y especialización
- **Monthly Meetups**: Virtual y presenciales en capitales LATAM
- **Agent Marketplace**: Comparte y monetiza tus agentes

### Contribution Guidelines
```markdown
## Contribuir a EnbabelLATAM

1. **Diversidad Cultural**: Celebramos todas las culturas LATAM
2. **Accesibilidad**: Priorizamos soluciones de bajo costo
3. **Documentación**: Siempre en español/português + inglés
4. **Testing**: Incluye casos de prueba culturalmente relevantes
5. **Community First**: El beneficio comunitario sobre el individual
```

### Open Source Spirit
```kotlin
/**
 * En el espíritu de la "minga" - trabajo comunitario para beneficio colectivo
 * Todos los agentes contribuidos a este proyecto son libres para uso
 * de la comunidad LATAM, con prioridad para:
 * - Startups LATAM
 * - Proyectos de impacto social
 * - Iniciativas educativas
 * - Organizaciones sin fines de lucro
 */
@OpenSource(license = "MIT", priority = "LATAM_COMMUNITY")
```

---

## 🔮 Roadmap LATAM

### Q2 2025: Fundación
- [x] Fork funcional de Embabel
- [x] Integración básica multiidioma
- [ ] Agentes MVP (MercadoLibre, Fintech, Content)
- [ ] Documentación completa en español
- [ ] Primera comunidad de 100 desarrolladores

### Q3 2025: Expansión
- [ ] Soporte para 10 países LATAM
- [ ] Marketplace de agentes
- [ ] Integración con APIs bancarias locales
- [ ] Workshops presenciales en 5 ciudades

### Q4 2025: Madurez
- [ ] Federación cross-border de agentes
- [ ] Certificaciones profesionales
- [ ] Partnerships con universidades LATAM
- [ ] 1000+ agentes desplegados en producción

### 2026: Expansión Global
- [ ] Bridge entre LATAM y otros mercados emergentes
- [ ] Influencia en estándares globales de AI
- [ ] EnbabelLATAM como referencia mundial
- [ ] Impacto medible en economías LATAM

---

## 🎵 Cultural Touch

### Poetry in Code
```kotlin
/**
 * "En Babel confundieron las lenguas,
 * en EnbabelLATAM las unificamos.
 * No para construir torres al cielo,
 * sino puentes entre hermanos."
 * 
 * - Luisfe Sorret, Fundador EnbabelLATAM
 */
@Poesia(autor = "LuisfeSorret", tipo = "Inspiracional")
class VisionLatam
```

### Regional Flavors
```kotlin
enum class SaborRegional {
    PICANTE_MEXICANO("🌶️ Con sabor a chile y mezcal"),
    TANGO_ARGENTINO("🎵 Con la pasión del tango"),
    SAMBA_BRASILEÑO("🎊 Con energía de carnaval"),
    SALSA_COLOMBIANA("💃 Con ritmo y sabrosura"),
    MARIACHI_TRADITIONS("🎺 Con tradición y orgullo")
}
```

---

## 📞 Support & Contact

### Technical Support
- **GitHub Issues**: Para bugs y feature requests
- **Documentation**: [Wiki EnbabelLATAM](https://github.com/SorretAI/enbabel-agent_LATAM/wiki)
- **Stack Overflow**: Tag `enbabel-latam`

### Community
- **Telegram**: @EnbabelLATAM
- **LinkedIn**: EnbabelLATAM Community
- **Twitter/X**: @EnbabelLATAM

### Business Inquiries
- **Email**: hola@enbabel-latam.com
- **WhatsApp Business**: +52-55-ENBABEL (362-2235)

---

## 🏆 Hall of Fame

### Contributors LATAM
- **Luisfe Sorret** 🇸🇻 - Founder & Architect
- **[Tu nombre aquí]** 🇲🇽🇦🇷🇧🇷🇨🇴🇨🇱🇵🇪🇺🇾🇪🇨🇧🇴🇵🇾🇻🇪 - Community Builder

### Agent Creators
- **MercadoLibre Agent**: @luisfesorret
- **Banking Agent**: TBD - ¡Podría ser tuyo!
- **Cultural Events Agent**: TBD - ¡Contribuye!

---

## 🎪 Final Words

**EnbabelLATAM** no es solo un fork técnico - es un movimiento cultural. Estamos construyendo el futuro de la AI para América Latina, con la sabiduría ancestral de nuestros pueblos y la innovación tecnológica del siglo XXI.

*"Juntos somos más fuertes. En Babel, LATAM, construimos puentes."*

---

**© 2025 EnbabelLATAM Community**  
*Built with ❤️ from El Salvador to Argentina*  
*Powered by Embabel Framework & LATAM Spirit*

**License**: MIT + Community Priority for LATAM  
**Version**: 1.0.0-LATAM  
**Last Update**: Junio 26, 2025

---

*¡Vamos a revolucionar la AI en América Latina! 🚀🌎*
